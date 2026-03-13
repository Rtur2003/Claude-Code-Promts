# Example: Performance Optimization for an E-Commerce API

> Real-world walkthrough of optimizing a slow API using the APEI cycle with **Agent System** + **Performance Optimization** prompts.

## Context

**Task**: An e-commerce API's product listing endpoint has degraded from 200ms to 3.5s response time as the product catalog grew to 500K items. Users are complaining and conversion rates are dropping.

**Prompts Used**: `claude-agent-system-prompt.md` + `performance-optimization-prompt.md`

---

## Iteration 1: Profiling & Quick Wins

### ANALYZE

```markdown
## Current State
- Endpoint: GET /api/products?category=electronics&sort=price&page=1
- Response time: 3.5s (p95), was 200ms 6 months ago
- Database: PostgreSQL 15, 500K products, 50 categories
- Stack: Node.js + Express + Prisma ORM
- Traffic: ~2,000 req/min during peak hours
- Server: 2 vCPU, 4GB RAM, single instance

## Symptoms
- All product listing pages are slow
- Category pages with sorting are worst
- Database CPU spikes to 90% during peak
- No caching layer exists
```

### PLAN

```markdown
## Optimization Plan
1. Profile the database — identify slow queries
2. Add missing indexes on frequently queried columns
3. Optimize the Prisma query — avoid N+1
4. Add response caching with Redis
5. Implement cursor-based pagination
```

### EXECUTE

#### 1. Database Profiling

```sql
-- Enable slow query logging
ALTER SYSTEM SET log_min_duration_statement = 100; -- Log queries > 100ms
SELECT pg_reload_conf();

-- Find the slowest queries
SELECT query, calls, mean_exec_time, total_exec_time
FROM pg_stat_statements
ORDER BY mean_exec_time DESC
LIMIT 10;

-- Result: The product listing query takes 2.8s average
-- EXPLAIN ANALYZE the problematic query
EXPLAIN (ANALYZE, BUFFERS, FORMAT TEXT)
SELECT p.*, c.name as category_name, 
       (SELECT AVG(rating) FROM reviews r WHERE r.product_id = p.id) as avg_rating,
       (SELECT COUNT(*) FROM reviews r WHERE r.product_id = p.id) as review_count
FROM products p
JOIN categories c ON c.id = p.category_id
WHERE p.category_id = 5
  AND p.is_active = true
ORDER BY p.price ASC
LIMIT 20 OFFSET 0;

-- Problems found:
-- 1. Sequential scan on products (no index on category_id + is_active)
-- 2. Correlated subqueries for reviews (N+1 pattern in SQL!)
-- 3. OFFSET-based pagination will get slower as pages increase
```

#### 2. Add Missing Indexes

```sql
-- Composite index for the most common query pattern
CREATE INDEX CONCURRENTLY idx_products_category_active_price 
ON products (category_id, is_active, price) 
WHERE is_active = true;

-- Index for review aggregation
CREATE INDEX CONCURRENTLY idx_reviews_product_id 
ON reviews (product_id);

-- Verify improvement
EXPLAIN (ANALYZE, BUFFERS)
SELECT * FROM products 
WHERE category_id = 5 AND is_active = true 
ORDER BY price ASC LIMIT 20;

-- Result: Seq Scan → Index Scan, 2.8s → 45ms ✅
```

#### 3. Eliminate N+1 with JOIN + Aggregation

```typescript
// ❌ Before: Prisma query with N+1 subqueries
const products = await prisma.product.findMany({
  where: { categoryId: 5, isActive: true },
  include: {
    category: true,
    reviews: true, // Loads ALL reviews for each product!
  },
  orderBy: { price: 'asc' },
  take: 20,
  skip: 0,
});

// Then computing averages in JS
const result = products.map(p => ({
  ...p,
  avgRating: p.reviews.reduce((sum, r) => sum + r.rating, 0) / p.reviews.length,
  reviewCount: p.reviews.length,
}));
```

```typescript
// ✅ After: Single optimized query with pre-computed aggregates
const products = await prisma.$queryRaw`
  SELECT p.id, p.name, p.price, p.image_url, p.slug,
         c.name as category_name,
         COALESCE(ra.avg_rating, 0) as avg_rating,
         COALESCE(ra.review_count, 0) as review_count
  FROM products p
  JOIN categories c ON c.id = p.category_id
  LEFT JOIN LATERAL (
    SELECT AVG(rating)::numeric(3,2) as avg_rating, 
           COUNT(*)::int as review_count
    FROM reviews r 
    WHERE r.product_id = p.id
  ) ra ON true
  WHERE p.category_id = ${categoryId}
    AND p.is_active = true
  ORDER BY p.price ASC
  LIMIT ${pageSize}
  OFFSET ${offset}
`;

// Result: 45ms → 12ms (eliminated N+1) ✅
```

### ITERATE

```
✅ Database indexes added → 2.8s → 45ms
✅ N+1 eliminated → 45ms → 12ms
✅ Query optimized with LATERAL JOIN

⚠️ Still needs:
1. No caching — same query hits DB every time
2. OFFSET pagination will slow down on page 1000+
3. No CDN for static product images
```

---

## Iteration 2: Caching & Pagination

### EXECUTE

#### 4. Redis Caching Layer

```typescript
// src/lib/cache.ts
import { Redis } from 'ioredis';

const redis = new Redis(process.env.REDIS_URL);

interface CacheOptions {
  ttl: number;       // seconds
  prefix: string;
  staleWhileRevalidate?: number; // serve stale, refresh in background
}

async function withCache<T>(
  key: string,
  fetcher: () => Promise<T>,
  options: CacheOptions,
): Promise<T> {
  const cacheKey = `${options.prefix}:${key}`;
  
  // Try cache first
  const cached = await redis.get(cacheKey);
  if (cached) {
    const parsed = JSON.parse(cached);
    
    // Check if stale but within revalidation window
    if (parsed._cachedAt && options.staleWhileRevalidate) {
      const age = (Date.now() - parsed._cachedAt) / 1000;
      if (age > options.ttl && age < options.ttl + options.staleWhileRevalidate) {
        // Serve stale, refresh in background
        fetcher().then(fresh => {
          redis.setex(cacheKey, options.ttl + (options.staleWhileRevalidate || 0), 
            JSON.stringify({ ...fresh, _cachedAt: Date.now() }));
        });
      }
    }
    
    delete parsed._cachedAt;
    return parsed as T;
  }
  
  // Cache miss — fetch and cache
  const data = await fetcher();
  await redis.setex(
    cacheKey, 
    options.ttl + (options.staleWhileRevalidate || 0),
    JSON.stringify({ ...data, _cachedAt: Date.now() }),
  );
  
  return data;
}

// Cache invalidation on product changes
async function invalidateProductCache(categoryId: number): Promise<void> {
  const keys = await redis.keys(`products:cat:${categoryId}:*`);
  if (keys.length > 0) {
    await redis.del(...keys);
  }
}
```

```typescript
// src/routes/products.ts — Using the cache
app.get('/api/products', async (req, res) => {
  const { category, sort = 'price', page = '1' } = req.query;
  const pageNum = parseInt(page as string);
  const cacheKey = `cat:${category}:sort:${sort}:page:${pageNum}`;
  
  const result = await withCache(
    cacheKey,
    () => fetchProducts({ categoryId: Number(category), sort, page: pageNum }),
    {
      prefix: 'products',
      ttl: 300,                   // 5 min cache
      staleWhileRevalidate: 60,   // Serve stale for 1 min while refreshing
    },
  );
  
  res.json(result);
});

// Result: 12ms (DB) → 1-2ms (cache hit) for 95% of requests ✅
```

#### 5. Cursor-Based Pagination

```typescript
// ❌ Before: OFFSET pagination (gets slower with higher pages)
// Page 1: OFFSET 0  → fast
// Page 100: OFFSET 1980 → slow (DB scans & discards 1980 rows)

// ✅ After: Cursor-based pagination (constant time regardless of page)
interface PaginatedResult<T> {
  items: T[];
  cursor: string | null;
  hasMore: boolean;
}

async function fetchProductsCursor(params: {
  categoryId: number;
  sort: string;
  cursor?: string;
  limit: number;
}): Promise<PaginatedResult<Product>> {
  const { categoryId, sort, cursor, limit } = params;
  
  let cursorCondition = '';
  if (cursor) {
    const decoded = JSON.parse(Buffer.from(cursor, 'base64url').toString());
    // Cursor encodes the last seen value for stable pagination
    cursorCondition = `AND (p.price, p.id) > (${decoded.price}, ${decoded.id})`;
  }
  
  const products = await prisma.$queryRawUnsafe(`
    SELECT p.id, p.name, p.price, p.image_url, p.slug,
           c.name as category_name,
           COALESCE(ra.avg_rating, 0) as avg_rating,
           COALESCE(ra.review_count, 0) as review_count
    FROM products p
    JOIN categories c ON c.id = p.category_id
    LEFT JOIN LATERAL (
      SELECT AVG(rating)::numeric(3,2) as avg_rating, 
             COUNT(*)::int as review_count
      FROM reviews r WHERE r.product_id = p.id
    ) ra ON true
    WHERE p.category_id = $1
      AND p.is_active = true
      ${cursorCondition}
    ORDER BY p.price ASC, p.id ASC
    LIMIT $2
  `, categoryId, limit + 1); // Fetch one extra to check hasMore
  
  const hasMore = products.length > limit;
  const items = products.slice(0, limit);
  
  const lastItem = items[items.length - 1];
  const nextCursor = hasMore && lastItem
    ? Buffer.from(JSON.stringify({ price: lastItem.price, id: lastItem.id })).toString('base64url')
    : null;
  
  return { items, cursor: nextCursor, hasMore };
}

// Result: Page 1000 now takes 12ms instead of 800ms ✅
```

### ITERATE

```
✅ Redis caching — 95% cache hit rate, 1-2ms response
✅ Stale-while-revalidate — Users never see slow responses
✅ Cursor pagination — Constant time regardless of page depth
✅ Cache invalidation on product updates

📊 Final Performance Comparison:

| Metric         | Before  | After    | Improvement |
|----------------|---------|----------|-------------|
| p50 response   | 2.1s    | 3ms      | 700x faster |
| p95 response   | 3.5s    | 15ms     | 233x faster |
| p99 response   | 5.2s    | 45ms     | 115x faster |
| DB CPU (peak)  | 90%     | 15%      | 6x reduction|
| Cache hit rate  | 0%     | 95%      | —           |
| Throughput      | 200/s   | 5,000/s  | 25x more    |

✅ All targets met:
- Response time < 50ms (p95) — achieved 15ms
- Handle 5,000 req/s — achieved
- DB CPU < 30% at peak — achieved 15%
```

---

## Key Takeaways

1. **Profile first**: Don't guess — use `EXPLAIN ANALYZE` and `pg_stat_statements` to find the actual bottleneck
2. **Index strategically**: Composite indexes matching your WHERE + ORDER BY pattern make the biggest impact
3. **Eliminate N+1**: The most common API performance killer — always check for it
4. **Cache aggressively**: Most product pages don't change frequently — cache with stale-while-revalidate
5. **Cursor pagination**: OFFSET breaks at scale — cursor-based pagination is O(1) regardless of page depth
6. **Measure everything**: Before/after metrics prove the value and catch regressions
