# Example: Express.js to NestJS Migration

> Real-world walkthrough of migrating a production API from Express.js to NestJS using the APEI cycle with **Agent System** + **Migration & Upgrade** prompts.

## Context

**Task**: A 3-year-old Express.js API has grown to 60+ endpoints with inconsistent patterns, no dependency injection, and tangled middleware. The team wants to migrate to NestJS for better structure, built-in validation, and TypeScript-first development — without any downtime.

**Prompts Used**: `claude-agent-system-prompt.md` + `migration-upgrade-prompt.md`

---

## Iteration 1: Assessment & Strategy

### ANALYZE

```markdown
## Current State
- Framework: Express.js 4.18 + TypeScript (loosely typed)
- Endpoints: 62 REST endpoints across 8 domains
- Database: PostgreSQL with Prisma ORM (keeping this)
- Auth: Custom JWT middleware (roles: admin, user, manager)
- Middleware: 12 custom middleware functions (logging, CORS, rate limiting, etc.)
- Tests: 45 integration tests (supertest), 30% coverage
- Traffic: ~5,000 req/min, 99.9% uptime SLA
- Team: 4 developers, 2 familiar with NestJS

## Pain Points
- No consistent request validation → runtime errors
- Middleware execution order is fragile and undocumented
- No dependency injection → hard to test, tight coupling
- Route definitions scattered across files
- Error handling inconsistent across endpoints

## Constraints
- Zero downtime during migration
- Existing tests must keep passing throughout
- Prisma ORM stays (no DB changes)
- Migration must complete within 3 sprints (6 weeks)
```

### PLAN

```markdown
## Migration Strategy: Strangler Fig Pattern

Migrate incrementally behind a reverse proxy. New NestJS service handles
migrated routes; Express handles the rest. Route by route, no big bang.

### Phase Plan
1. Set up NestJS project alongside Express (parallel running)
2. Configure reverse proxy to route traffic to both services
3. Migrate shared infrastructure (auth, validation, error handling)
4. Migrate domains one by one (users → products → orders → ...)
5. Decommission Express after all routes migrated

### Risk Mitigation
- Feature flags to toggle between Express and NestJS per route
- Automated comparison testing (same request → both services → compare responses)
- Rollback plan: proxy reverts to Express for any failing route
```

### EXECUTE

#### 1. NestJS Project Setup (Alongside Express)

```
project/
├── apps/
│   ├── express-api/          # Existing Express app (unchanged)
│   │   ├── src/
│   │   └── package.json
│   └── nestjs-api/           # New NestJS app
│       ├── src/
│       │   ├── main.ts
│       │   ├── app.module.ts
│       │   └── common/       # Shared modules
│       └── package.json
├── packages/
│   └── shared/               # Shared types, constants, Prisma client
│       ├── src/
│       └── package.json
├── docker-compose.yml        # Both services + proxy
└── package.json              # Workspace root
```

```typescript
// apps/nestjs-api/src/main.ts
import { NestFactory } from '@nestjs/core';
import { ValidationPipe } from '@nestjs/common';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // Global validation pipe — validates ALL incoming requests
  app.setGlobalPrefix('api');
  app.useGlobalPipes(new ValidationPipe({
    whitelist: true,          // Strip unknown properties
    forbidNonWhitelisted: true, // Throw on unknown properties
    transform: true,          // Auto-transform types
    transformOptions: {
      enableImplicitConversion: true,
    },
  }));

  await app.listen(3001); // Different port from Express (3000)
}
bootstrap();
```

#### 2. Reverse Proxy Configuration

```nginx
# nginx.conf — Route-level traffic splitting
upstream express_api {
    server express-api:3000;
}

upstream nestjs_api {
    server nestjs-api:3001;
}

server {
    listen 80;

    # Migrated routes → NestJS
    location /api/users {
        proxy_pass http://nestjs_api;
    }

    # Not yet migrated → Express
    location /api/ {
        proxy_pass http://express_api;
    }

    # Health checks for both
    location /health/express {
        proxy_pass http://express_api/health;
    }
    location /health/nestjs {
        proxy_pass http://nestjs_api/health;
    }
}
```

### ITERATE

```
✅ NestJS project initialized alongside Express
✅ Both services run simultaneously (ports 3000 & 3001)
✅ Nginx proxy configured for route-level splitting
✅ Shared Prisma client extracted to packages/shared
✅ Health checks verified for both services

⚠️ Ready for first domain migration (users)
```

---

## Iteration 2: Migrating Auth & First Domain

### EXECUTE

#### 3. Auth Guard (Express Middleware → NestJS Guard)

```typescript
// EXPRESS (before) — Custom middleware
// apps/express-api/src/middleware/auth.ts
function authMiddleware(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'No token' });

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    // 🐛 Bug: silently passes for some error types
    if (err.name === 'TokenExpiredError') {
      return res.status(401).json({ error: 'Token expired' });
    }
    next(); // ← Bug: invalid tokens pass through!
  }
}
```

```typescript
// NESTJS (after) — Guard with proper error handling
// apps/nestjs-api/src/common/guards/auth.guard.ts
import { CanActivate, ExecutionContext, Injectable, UnauthorizedException } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';
import { Reflector } from '@nestjs/core';

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(
    private jwtService: JwtService,
    private reflector: Reflector,
  ) {}

  async canActivate(context: ExecutionContext): Promise<boolean> {
    // Check if route is public (skip auth)
    const isPublic = this.reflector.get<boolean>('isPublic', context.getHandler());
    if (isPublic) return true;

    const request = context.switchToHttp().getRequest();
    const token = this.extractToken(request);

    if (!token) {
      throw new UnauthorizedException('Authentication required');
    }

    try {
      const payload = await this.jwtService.verifyAsync(token);
      request.user = payload;
    } catch (error) {
      // ✅ Fix: ALL invalid tokens are rejected (not just expired)
      if (error.name === 'TokenExpiredError') {
        throw new UnauthorizedException('Token has expired');
      }
      throw new UnauthorizedException('Invalid authentication token');
    }

    return true;
  }

  private extractToken(request: any): string | null {
    const [type, token] = request.headers.authorization?.split(' ') ?? [];
    return type === 'Bearer' ? token : null;
  }
}

// Role-based access control decorator
import { SetMetadata } from '@nestjs/common';
export const Roles = (...roles: string[]) => SetMetadata('roles', roles);
export const Public = () => SetMetadata('isPublic', true);
```

#### 4. First Domain Migration — Users

```typescript
// EXPRESS (before) — Route definitions
// apps/express-api/src/routes/users.ts
router.get('/users', authMiddleware, async (req, res) => {
  try {
    const users = await prisma.user.findMany({
      take: parseInt(req.query.limit) || 20,  // ← No validation!
      skip: parseInt(req.query.offset) || 0,
    });
    res.json(users);
  } catch (err) {
    res.status(500).json({ error: 'Internal error' }); // ← Generic error
  }
});

router.get('/users/:id', authMiddleware, async (req, res) => {
  const user = await prisma.user.findUnique({ where: { id: req.params.id } });
  if (!user) return res.status(404).json({ error: 'Not found' });
  res.json(user);
});

router.post('/users', authMiddleware, roleCheck('admin'), async (req, res) => {
  // ← No body validation!
  const user = await prisma.user.create({ data: req.body });
  res.status(201).json(user);
});
```

```typescript
// NESTJS (after) — Controller with validation & DTOs
// apps/nestjs-api/src/modules/users/users.controller.ts
import { Controller, Get, Post, Param, Query, Body, ParseUUIDPipe } from '@nestjs/common';
import { UsersService } from './users.service';
import { CreateUserDto, ListUsersDto, UserResponseDto } from './users.dto';
import { Roles } from '@/common/guards/auth.guard';

@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  async list(@Query() query: ListUsersDto): Promise<UserResponseDto[]> {
    return this.usersService.findAll(query);
  }

  @Get(':id')
  async findOne(@Param('id', ParseUUIDPipe) id: string): Promise<UserResponseDto> {
    return this.usersService.findOneOrFail(id);
  }

  @Post()
  @Roles('admin')
  async create(@Body() dto: CreateUserDto): Promise<UserResponseDto> {
    return this.usersService.create(dto);
  }
}
```

```typescript
// apps/nestjs-api/src/modules/users/users.dto.ts
import { IsEmail, IsString, MinLength, IsOptional, IsInt, Min, Max } from 'class-validator';
import { Type, Exclude, Expose } from 'class-transformer';

export class CreateUserDto {
  @IsEmail()
  email: string;

  @IsString()
  @MinLength(2)
  name: string;

  @IsString()
  @MinLength(8)
  password: string;
}

export class ListUsersDto {
  @IsOptional()
  @Type(() => Number)
  @IsInt()
  @Min(1)
  @Max(100)
  limit: number = 20;

  @IsOptional()
  @Type(() => Number)
  @IsInt()
  @Min(0)
  offset: number = 0;
}

// Response DTO — exclude sensitive fields
export class UserResponseDto {
  @Expose() id: string;
  @Expose() email: string;
  @Expose() name: string;
  @Expose() role: string;
  @Expose() createdAt: Date;
  @Exclude() passwordHash: never; // Never exposed
}
```

```typescript
// apps/nestjs-api/src/modules/users/users.service.ts
import { Injectable, NotFoundException, ConflictException } from '@nestjs/common';
import { PrismaService } from '@/common/prisma/prisma.service';
import { CreateUserDto, ListUsersDto } from './users.dto';
import * as bcrypt from 'bcrypt';

@Injectable()
export class UsersService {
  constructor(private prisma: PrismaService) {}

  async findAll(query: ListUsersDto) {
    return this.prisma.user.findMany({
      take: query.limit,
      skip: query.offset,
      select: { id: true, email: true, name: true, role: true, createdAt: true },
      orderBy: { createdAt: 'desc' },
    });
  }

  async findOneOrFail(id: string) {
    const user = await this.prisma.user.findUnique({
      where: { id },
      select: { id: true, email: true, name: true, role: true, createdAt: true },
    });
    if (!user) throw new NotFoundException(`User not found: ${id}`);
    return user;
  }

  async create(dto: CreateUserDto) {
    const existing = await this.prisma.user.findUnique({
      where: { email: dto.email },
    });
    if (existing) throw new ConflictException('Email already registered');

    const passwordHash = await bcrypt.hash(dto.password, 12);
    return this.prisma.user.create({
      data: { email: dto.email, name: dto.name, passwordHash },
      select: { id: true, email: true, name: true, role: true, createdAt: true },
    });
  }
}
```

#### 5. Comparison Testing

```typescript
// tests/comparison/users.comparison.test.ts
// Run same requests against both services, compare responses
import { describe, it, expect } from 'vitest';
import request from 'supertest';

const EXPRESS_URL = 'http://localhost:3000';
const NESTJS_URL = 'http://localhost:3001';

describe('Express ↔ NestJS comparison: Users', () => {
  it('GET /api/users returns identical data', async () => {
    const [expressRes, nestRes] = await Promise.all([
      request(EXPRESS_URL).get('/api/users').set('Authorization', `Bearer ${testToken}`),
      request(NESTJS_URL).get('/api/users').set('Authorization', `Bearer ${testToken}`),
    ]);

    expect(expressRes.status).toBe(nestRes.status);
    expect(expressRes.body.length).toBe(nestRes.body.length);

    // Compare each user (NestJS may exclude extra fields — that's expected)
    for (let i = 0; i < expressRes.body.length; i++) {
      expect(nestRes.body[i].id).toBe(expressRes.body[i].id);
      expect(nestRes.body[i].email).toBe(expressRes.body[i].email);
      expect(nestRes.body[i].name).toBe(expressRes.body[i].name);
    }
  });

  it('GET /api/users/:id returns identical data for valid ID', async () => {
    const userId = 'known-test-user-id';
    const [expressRes, nestRes] = await Promise.all([
      request(EXPRESS_URL).get(`/api/users/${userId}`).set('Authorization', `Bearer ${testToken}`),
      request(NESTJS_URL).get(`/api/users/${userId}`).set('Authorization', `Bearer ${testToken}`),
    ]);

    expect(expressRes.status).toBe(nestRes.status);
    expect(nestRes.body.id).toBe(expressRes.body.id);
  });

  it('GET /api/users/:id returns same error for invalid ID', async () => {
    const [expressRes, nestRes] = await Promise.all([
      request(EXPRESS_URL).get('/api/users/nonexistent').set('Authorization', `Bearer ${testToken}`),
      request(NESTJS_URL).get('/api/users/nonexistent').set('Authorization', `Bearer ${testToken}`),
    ]);

    // Both should return 404 (or 400 for invalid UUID format in NestJS)
    expect([400, 404]).toContain(nestRes.status);
  });
});
```

### ITERATE

```
✅ Auth guard migrated — fixed silent token passthrough bug
✅ Users domain fully migrated (3 endpoints)
   - GET /api/users — with validated pagination
   - GET /api/users/:id — with UUID validation
   - POST /api/users — with DTO validation + duplicate check
✅ Comparison tests confirm parity between Express and NestJS
✅ Proxy updated to route /api/users/* → NestJS
✅ Existing Express tests still pass (unchanged routes unaffected)

📊 Migration Progress:

| Domain      | Endpoints | Status        |
|-------------|-----------|---------------|
| Users       | 8         | ✅ Migrated   |
| Auth        | 4         | ✅ Migrated   |
| Products    | 12        | ⏳ Next       |
| Orders      | 15        | ⬜ Pending    |
| Payments    | 6         | ⬜ Pending    |
| Inventory   | 8         | ⬜ Pending    |
| Reports     | 5         | ⬜ Pending    |
| Admin       | 4         | ⬜ Pending    |
| **Total**   | **62**    | **12/62 (19%)**|

⚠️ Bugs fixed during migration:
1. Auth middleware silently passed invalid tokens (not just expired)
2. No input validation on user listing (limit/offset could be negative or huge)
3. Password hash was exposed in some user list responses
```

---

## Iteration 3: Remaining Domains & Decommission

### EXECUTE (Summary)

The remaining domains followed the same pattern:

1. Create NestJS module (controller + service + DTOs)
2. Add request validation via `class-validator` decorators
3. Run comparison tests against both services
4. Update proxy to route to NestJS
5. Monitor error rates and latency for 48 hours
6. Mark domain as fully migrated

#### Key Improvements Gained During Migration

```typescript
// ✅ Global exception filter (consistent error format)
@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse();

    const status = exception instanceof HttpException
      ? exception.getStatus()
      : 500;

    const message = exception instanceof HttpException
      ? exception.getResponse()
      : 'Internal server error';

    response.status(status).json({
      error: {
        statusCode: status,
        message: typeof message === 'string' ? message : (message as any).message,
        timestamp: new Date().toISOString(),
      },
    });
  }
}

// ✅ Request logging interceptor (replaces 3 Express middleware)
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest();
    const start = Date.now();

    return next.handle().pipe(
      tap(() => {
        const duration = Date.now() - start;
        logger.info(`${request.method} ${request.url} ${duration}ms`);
      }),
    );
  }
}
```

### ITERATE

```
📊 Final Migration Summary:

| Metric              | Express (Before) | NestJS (After) | Change       |
|---------------------|------------------|----------------|--------------|
| Endpoints           | 62               | 62             | Same         |
| Input validation    | 5 endpoints      | 62 endpoints   | 100% coverage|
| Test coverage       | 30%              | 78%            | +48%         |
| Avg response time   | 45ms             | 42ms           | 7% faster    |
| Error rate          | 0.3%             | 0.08%          | 73% fewer    |
| Bugs fixed          | —                | 7              | —            |
| Downtime            | —                | 0              | Zero downtime|
| Migration duration  | —                | 5 weeks        | Under budget |

✅ All 62 endpoints migrated to NestJS
✅ Zero downtime throughout migration
✅ All existing tests passing on new service
✅ 7 bugs found and fixed during migration
✅ Express service decommissioned
✅ Proxy simplified to single upstream
```

---

## Key Takeaways

1. **Strangler Fig Pattern**: Never rewrite from scratch — migrate route by route behind a proxy, ensuring zero downtime and easy rollback
2. **Comparison testing**: Run the same requests against both old and new services to verify behavioral parity before switching traffic
3. **Fix bugs during migration**: Migration is the best time to fix long-standing issues — you're already touching every endpoint
4. **DTOs + validation are free wins**: NestJS's `class-validator` catches entire categories of bugs that Express middleware missed
5. **Shared packages**: Extract shared code (Prisma client, types, constants) into a shared package to avoid duplication between services
6. **Monitor after each switch**: Wait 48 hours after routing traffic to the new service before marking a domain as complete
7. **Auth guard > middleware**: NestJS guards are more explicit about what's protected and what's public — reduces the "silent passthrough" class of bugs
