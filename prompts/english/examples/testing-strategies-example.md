# Example: Testing Strategy for a Legacy Express API

> Real-world walkthrough of adding comprehensive tests to an untested API using the APEI cycle with **Agent System** + **Testing Strategies** prompts.

## Context

**Task**: A legacy Express.js REST API has 0% test coverage. Users report random bugs after every deploy. The team wants to reach 80% coverage and implement CI checks before any new features are built.

**Prompts Used**: `claude-agent-system-prompt.md` + `testing-strategies-prompt.md`

---

## Iteration 1: Assessment & Unit Test Foundation

### ANALYZE

```markdown
## Current State
- API: Express.js + TypeScript, 45 endpoints, ~8K LOC
- Database: PostgreSQL with Prisma ORM
- Auth: JWT-based, custom middleware
- Test coverage: 0% — no test files exist
- Test infrastructure: None — no runner, no mocking, no CI
- Deploy: Manual via SSH → frequent regressions
- Key pain points:
  - User registration sometimes creates duplicate accounts
  - Order total calculations off by cents on some currency combos
  - Auth middleware silently fails for expired tokens

## Critical Business Logic
- User registration & authentication
- Order creation & total calculation  
- Payment processing (Stripe integration)
- Inventory management (stock deduction)
```

### PLAN

```markdown
## Testing Strategy
1. Set up test infrastructure (Vitest, fixtures, mocking)
2. Unit test critical business logic (registration, orders, payments)
3. Integration test API endpoints (auth, CRUD, edge cases)
4. Add CI pipeline with coverage gates
5. Implement contract tests for Stripe integration
```

### EXECUTE

#### 1. Test Infrastructure Setup

```bash
# Install testing dependencies
npm install -D vitest @vitest/coverage-v8 supertest @types/supertest
npm install -D @faker-js/faker testcontainers
```

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';
import path from 'path';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
    setupFiles: ['./tests/setup.ts'],
    include: ['tests/**/*.test.ts'],
    coverage: {
      provider: 'v8',
      reporter: ['text', 'lcov', 'html'],
      exclude: ['tests/**', 'prisma/**', 'dist/**'],
      thresholds: {
        branches: 80,
        functions: 80,
        lines: 80,
        statements: 80,
      },
    },
    // Run tests sequentially (DB tests need isolation)
    pool: 'forks',
    poolOptions: {
      forks: { singleFork: true },
    },
  },
  resolve: {
    alias: { '@': path.resolve(__dirname, 'src') },
  },
});
```

```typescript
// tests/setup.ts
import { beforeAll, afterAll, afterEach } from 'vitest';
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

beforeAll(async () => {
  // Use test database
  process.env.DATABASE_URL = process.env.TEST_DATABASE_URL;
  await prisma.$connect();
});

afterEach(async () => {
  // Clean all tables between tests (maintain isolation)
  const tables = await prisma.$queryRaw<{ tablename: string }[]>`
    SELECT tablename FROM pg_tables WHERE schemaname = 'public'
  `;
  for (const { tablename } of tables) {
    if (tablename !== '_prisma_migrations') {
      await prisma.$executeRawUnsafe(`TRUNCATE TABLE "${tablename}" CASCADE`);
    }
  }
});

afterAll(async () => {
  await prisma.$disconnect();
});

export { prisma };
```

```typescript
// tests/factories.ts — Test data factories
import { faker } from '@faker-js/faker';
import { prisma } from './setup';
import bcrypt from 'bcrypt';

export async function createUser(overrides: Partial<{
  email: string;
  name: string;
  password: string;
}> = {}) {
  return prisma.user.create({
    data: {
      email: overrides.email ?? faker.internet.email(),
      name: overrides.name ?? faker.person.fullName(),
      passwordHash: await bcrypt.hash(overrides.password ?? 'TestPass123!', 10),
    },
  });
}

export async function createProduct(overrides: Partial<{
  name: string;
  price: number;
  stock: number;
}> = {}) {
  return prisma.product.create({
    data: {
      name: overrides.name ?? faker.commerce.productName(),
      price: overrides.price ?? parseFloat(faker.commerce.price({ min: 1, max: 1000 })),
      stock: overrides.stock ?? faker.number.int({ min: 0, max: 100 }),
      sku: faker.string.alphanumeric(10).toUpperCase(),
    },
  });
}
```

#### 2. Unit Tests — Critical Business Logic

```typescript
// tests/unit/order-calculator.test.ts
import { describe, it, expect } from 'vitest';
import { calculateOrderTotal } from '@/services/order-calculator';

describe('OrderCalculator', () => {
  describe('calculateOrderTotal', () => {
    it('calculates total for single item', () => {
      const result = calculateOrderTotal([
        { productId: '1', price: 29.99, quantity: 1 },
      ]);

      expect(result.subtotal).toBe(29.99);
      expect(result.tax).toBe(2.40); // 8% tax
      expect(result.total).toBe(32.39);
    });

    it('calculates total for multiple items', () => {
      const result = calculateOrderTotal([
        { productId: '1', price: 29.99, quantity: 2 },
        { productId: '2', price: 15.50, quantity: 1 },
      ]);

      expect(result.subtotal).toBe(75.48); // (29.99 * 2) + 15.50
      expect(result.total).toBe(81.52);     // 75.48 + 6.04 tax
    });

    // 🐛 Bug found! Floating point issue with certain prices
    it('handles floating point precision correctly', () => {
      const result = calculateOrderTotal([
        { productId: '1', price: 0.1, quantity: 3 },
        { productId: '2', price: 0.2, quantity: 1 },
      ]);

      // ❌ Without fix: 0.1 * 3 + 0.2 = 0.30000000000000004 + 0.2
      // ✅ With fix: should be exactly 0.50
      expect(result.subtotal).toBe(0.50);
      expect(result.tax).toBe(0.04);
      expect(result.total).toBe(0.54);
    });

    it('applies discount codes correctly', () => {
      const result = calculateOrderTotal(
        [{ productId: '1', price: 100, quantity: 1 }],
        { code: 'SAVE20', type: 'percentage', value: 20 },
      );

      expect(result.subtotal).toBe(100);
      expect(result.discount).toBe(20);
      expect(result.total).toBe(86.40); // (100 - 20) * 1.08
    });

    it('rejects negative quantities', () => {
      expect(() => calculateOrderTotal([
        { productId: '1', price: 29.99, quantity: -1 },
      ])).toThrow('Quantity must be positive');
    });

    it('rejects empty order', () => {
      expect(() => calculateOrderTotal([])).toThrow('Order must have at least one item');
    });
  });
});
```

```typescript
// tests/unit/auth-service.test.ts
import { describe, it, expect, vi, beforeEach } from 'vitest';
import { AuthService } from '@/services/auth-service';
import bcrypt from 'bcrypt';

describe('AuthService', () => {
  let authService: AuthService;
  let mockUserRepo: any;

  beforeEach(() => {
    mockUserRepo = {
      findByEmail: vi.fn(),
      create: vi.fn(),
      existsByEmail: vi.fn(),
    };
    authService = new AuthService(mockUserRepo);
  });

  describe('register', () => {
    it('creates user with hashed password', async () => {
      mockUserRepo.existsByEmail.mockResolvedValue(false);
      mockUserRepo.create.mockResolvedValue({ id: '1', email: 'test@test.com' });

      const result = await authService.register({
        email: 'test@test.com',
        name: 'Test User',
        password: 'SecurePass123!',
      });

      expect(result.ok).toBe(true);
      // Verify password was hashed (not stored plain)
      const createCall = mockUserRepo.create.mock.calls[0][0];
      expect(createCall.passwordHash).not.toBe('SecurePass123!');
      expect(await bcrypt.compare('SecurePass123!', createCall.passwordHash)).toBe(true);
    });

    // 🐛 Bug found! Duplicate registration race condition
    it('rejects duplicate email registration', async () => {
      mockUserRepo.existsByEmail.mockResolvedValue(true);

      const result = await authService.register({
        email: 'existing@test.com',
        name: 'Test',
        password: 'Pass123!',
      });

      expect(result.ok).toBe(false);
      expect(result.error?.code).toBe('EMAIL_EXISTS');
    });

    it('validates password strength', async () => {
      mockUserRepo.existsByEmail.mockResolvedValue(false);

      const result = await authService.register({
        email: 'test@test.com',
        name: 'Test',
        password: '123',  // too weak
      });

      expect(result.ok).toBe(false);
      expect(result.error?.code).toBe('WEAK_PASSWORD');
    });
  });

  describe('login', () => {
    it('returns tokens for valid credentials', async () => {
      const hash = await bcrypt.hash('ValidPass123!', 10);
      mockUserRepo.findByEmail.mockResolvedValue({
        id: '1',
        email: 'test@test.com',
        passwordHash: hash,
      });

      const result = await authService.login('test@test.com', 'ValidPass123!');

      expect(result.ok).toBe(true);
      expect(result.value).toHaveProperty('accessToken');
      expect(result.value).toHaveProperty('refreshToken');
    });

    it('rejects invalid password', async () => {
      const hash = await bcrypt.hash('CorrectPass', 10);
      mockUserRepo.findByEmail.mockResolvedValue({
        id: '1',
        passwordHash: hash,
      });

      const result = await authService.login('test@test.com', 'WrongPass');

      expect(result.ok).toBe(false);
      expect(result.error?.code).toBe('INVALID_CREDENTIALS');
    });

    it('rejects non-existent user with same timing', async () => {
      mockUserRepo.findByEmail.mockResolvedValue(null);

      const start = Date.now();
      const result = await authService.login('nonexistent@test.com', 'Pass123!');
      const duration = Date.now() - start;

      expect(result.ok).toBe(false);
      // Timing should be similar to valid user check (prevents user enumeration)
      expect(duration).toBeGreaterThan(50); // bcrypt compare takes time
    });
  });
});
```

### ITERATE

```
✅ Test infrastructure set up — Vitest + coverage + factories
✅ 12 unit tests written — all passing
✅ 2 bugs found and documented:
   - Floating point arithmetic in order calculations
   - No duplicate email check in registration flow
✅ Coverage for tested modules: 94% lines

⚠️ Still needs:
1. Integration tests for API endpoints
2. CI pipeline with coverage gates
3. Contract tests for Stripe
```

---

## Iteration 2: Integration Tests & CI

### EXECUTE

#### 3. Integration Tests — API Endpoints

```typescript
// tests/integration/auth.test.ts
import { describe, it, expect, beforeAll } from 'vitest';
import request from 'supertest';
import { app } from '@/app';
import { createUser } from '../factories';

describe('POST /api/auth/register', () => {
  it('creates a new user and returns tokens', async () => {
    const res = await request(app)
      .post('/api/auth/register')
      .send({
        email: 'new@example.com',
        name: 'New User',
        password: 'SecurePass123!',
      });

    expect(res.status).toBe(201);
    expect(res.body).toHaveProperty('accessToken');
    expect(res.body).toHaveProperty('refreshToken');
    expect(res.body.user.email).toBe('new@example.com');
    // Password should never be in response
    expect(res.body.user).not.toHaveProperty('password');
    expect(res.body.user).not.toHaveProperty('passwordHash');
  });

  it('returns 409 for duplicate email', async () => {
    await createUser({ email: 'exists@example.com' });

    const res = await request(app)
      .post('/api/auth/register')
      .send({
        email: 'exists@example.com',
        name: 'Duplicate',
        password: 'SecurePass123!',
      });

    expect(res.status).toBe(409);
    expect(res.body.error.code).toBe('EMAIL_EXISTS');
  });

  it('returns 400 for invalid email format', async () => {
    const res = await request(app)
      .post('/api/auth/register')
      .send({
        email: 'not-an-email',
        name: 'Test',
        password: 'SecurePass123!',
      });

    expect(res.status).toBe(400);
    expect(res.body.error.code).toBe('VALIDATION_ERROR');
  });
});

describe('POST /api/auth/login', () => {
  it('returns tokens for valid credentials', async () => {
    await createUser({ email: 'login@example.com', password: 'MyPass123!' });

    const res = await request(app)
      .post('/api/auth/login')
      .send({ email: 'login@example.com', password: 'MyPass123!' });

    expect(res.status).toBe(200);
    expect(res.body).toHaveProperty('accessToken');
  });

  it('returns 401 for wrong password', async () => {
    await createUser({ email: 'test@example.com', password: 'CorrectPass123!' });

    const res = await request(app)
      .post('/api/auth/login')
      .send({ email: 'test@example.com', password: 'WrongPass123!' });

    expect(res.status).toBe(401);
    expect(res.body.error.code).toBe('INVALID_CREDENTIALS');
    // Error message should NOT reveal whether user exists
    expect(res.body.error.message).not.toContain('user not found');
  });
});

describe('Protected routes', () => {
  it('returns 401 without auth header', async () => {
    const res = await request(app).get('/api/orders');

    expect(res.status).toBe(401);
  });

  it('returns 401 with expired token', async () => {
    // Generate a token that expired 1 hour ago
    const expiredToken = generateToken({ userId: '1' }, { expiresIn: '-1h' });

    const res = await request(app)
      .get('/api/orders')
      .set('Authorization', `Bearer ${expiredToken}`);

    expect(res.status).toBe(401);
    expect(res.body.error.code).toBe('TOKEN_EXPIRED');
  });
});
```

```typescript
// tests/integration/orders.test.ts
import { describe, it, expect } from 'vitest';
import request from 'supertest';
import { app } from '@/app';
import { createUser, createProduct } from '../factories';
import { generateToken } from '@/services/auth-service';

describe('POST /api/orders', () => {
  it('creates an order and deducts stock', async () => {
    const user = await createUser();
    const product = await createProduct({ price: 29.99, stock: 10 });
    const token = generateToken({ userId: user.id });

    const res = await request(app)
      .post('/api/orders')
      .set('Authorization', `Bearer ${token}`)
      .send({
        items: [{ productId: product.id, quantity: 2 }],
      });

    expect(res.status).toBe(201);
    expect(res.body.total).toBe(64.78); // (29.99 * 2) + tax
    expect(res.body.items).toHaveLength(1);
    expect(res.body.status).toBe('pending');

    // Verify stock was deducted
    const updatedProduct = await prisma.product.findUnique({
      where: { id: product.id },
    });
    expect(updatedProduct!.stock).toBe(8); // 10 - 2
  });

  it('rejects order when insufficient stock', async () => {
    const user = await createUser();
    const product = await createProduct({ stock: 1 });
    const token = generateToken({ userId: user.id });

    const res = await request(app)
      .post('/api/orders')
      .set('Authorization', `Bearer ${token}`)
      .send({
        items: [{ productId: product.id, quantity: 5 }],
      });

    expect(res.status).toBe(409);
    expect(res.body.error.code).toBe('INSUFFICIENT_STOCK');
  });

  it('handles concurrent orders correctly (no overselling)', async () => {
    const user = await createUser();
    const product = await createProduct({ stock: 1 });
    const token = generateToken({ userId: user.id });

    // Send two orders simultaneously for 1 item each (only 1 in stock)
    const [res1, res2] = await Promise.all([
      request(app)
        .post('/api/orders')
        .set('Authorization', `Bearer ${token}`)
        .send({ items: [{ productId: product.id, quantity: 1 }] }),
      request(app)
        .post('/api/orders')
        .set('Authorization', `Bearer ${token}`)
        .send({ items: [{ productId: product.id, quantity: 1 }] }),
    ]);

    // One should succeed, one should fail
    const statuses = [res1.status, res2.status].sort();
    expect(statuses).toEqual([201, 409]);

    // Stock should be exactly 0 (not negative)
    const updatedProduct = await prisma.product.findUnique({
      where: { id: product.id },
    });
    expect(updatedProduct!.stock).toBe(0);
  });
});
```

#### 4. CI Pipeline

```yaml
# .github/workflows/test.yml
name: Test

on:
  push:
    branches: [main]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_USER: test
          POSTGRES_PASSWORD: test
          POSTGRES_DB: testdb
        ports: ['5432:5432']
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm

      - run: npm ci
      - run: npx prisma migrate deploy
        env:
          DATABASE_URL: postgresql://test:test@localhost:5432/testdb

      - run: npm run test -- --coverage
        env:
          TEST_DATABASE_URL: postgresql://test:test@localhost:5432/testdb
          JWT_SECRET: test-secret-for-ci

      - name: Coverage gate
        run: |
          COVERAGE=$(npx vitest run --coverage --reporter=json | jq '.total.lines.pct')
          echo "Coverage: $COVERAGE%"
          if (( $(echo "$COVERAGE < 80" | bc -l) )); then
            echo "❌ Coverage below 80%"
            exit 1
          fi
```

### ITERATE

```
✅ 24 integration tests — all passing
✅ CI pipeline configured with PostgreSQL service
✅ Coverage gate: 80% minimum enforced
✅ 3 bugs caught by tests:
   - Floating point in order calculations → Fixed with integer cents
   - Duplicate registration race condition → Fixed with unique constraint
   - Expired token silent failure → Fixed with explicit error response

📊 Final Test Summary:

| Metric            | Before  | After     |
|-------------------|---------|-----------|
| Test coverage     | 0%      | 84%       |
| Unit tests        | 0       | 18        |
| Integration tests | 0       | 24        |
| Bugs found        | —       | 3 critical|
| CI pipeline       | None    | Full      |
| Deploys with bugs | ~40%    | < 5%      |

✅ All targets met:
- Coverage > 80% — achieved 84%
- Critical paths tested — auth, orders, payments
- CI enforced — no merge without passing tests
- 3 production bugs caught before they reach users again
```

---

## Key Takeaways

1. **Start with infrastructure**: Set up test runner, factories, and cleanup before writing a single test — it pays for itself immediately
2. **Test the bugs you know**: Start with the bugs users already reported — they make great test cases and prove value to the team
3. **Factories over fixtures**: Use factory functions that generate realistic test data — they make tests readable and maintainable
4. **Database isolation**: Truncate tables between tests — flaky tests due to shared state will destroy trust in the test suite
5. **Integration > mocks for APIs**: Use `supertest` to test real HTTP requests against the actual app — catches middleware and routing issues
6. **Concurrent scenarios**: Test race conditions explicitly — the order overselling bug was only caught by a concurrent test
7. **CI as safety net**: Once tests pass, add a CI pipeline immediately — it prevents regression from the very first merge
