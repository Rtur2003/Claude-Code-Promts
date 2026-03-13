# Best Practices & Customization Guide

> How to adapt, customize, and get the most out of Claude Code Prompts for your team.

---

## Customizing Prompts for Your Team

### Step 1: Start with the Right Base

| Team Size | Recommended Setup |
|-----------|-------------------|
| Solo developer | Agent System prompt → paste into CLAUDE.md |
| Small team (2-5) | Agent System + 1-2 specialist prompts |
| Medium team (5-20) | Agent System + project-type + team standards appendix |
| Large team (20+) | Agent System + monorepo + team-specific CLAUDE.md hierarchy |

### Step 2: Add Your Team Standards

Append a `## Team Standards` section to any prompt:

```markdown
## Team Standards

### Stack
- Frontend: Next.js 15, TypeScript, Tailwind CSS, shadcn/ui
- Backend: Node.js, Prisma, PostgreSQL
- Testing: Vitest (unit), Playwright (e2e)
- CI/CD: GitHub Actions
- Hosting: Vercel (frontend), Railway (backend)

### Conventions
- Commits: Conventional Commits (feat/fix/docs/refactor)
- Branches: feature/, bugfix/, hotfix/ prefixes
- PRs: Require 1 approval + passing CI
- Coverage: Minimum 80% for new code
- Style: Prettier + ESLint (auto-formatted on save)

### Architecture Decisions
- State management: Zustand (no Redux)
- API layer: tRPC for internal, REST for external
- Auth: NextAuth.js with Google OAuth
- Monitoring: Sentry for errors, Vercel Analytics for performance

### Things to Avoid
- No `any` types in TypeScript
- No console.log in production code
- No direct database queries outside repository layer
- No inline styles (use Tailwind classes)
```

### Step 3: Create a Team CLAUDE.md

Combine your base prompt + team standards into a single CLAUDE.md:

```markdown
# CLAUDE.md

## About This Project
[Paste relevant sections from Agent System prompt]

## Team Standards
[Paste your team standards from Step 2]

## Project-Specific Context
[Add project-specific information:]
- Key domain terms and their meanings
- Important business rules
- Integration points with external services
- Known issues or technical debt to be aware of
```

---

## Prompt Composition Patterns

### Pattern 1: Single Prompt (Simple Projects)

```
CLAUDE.md = Agent System Prompt
```

Best for solo developers or simple projects. Gives you the full APEI cycle and code quality standards.

### Pattern 2: Base + Specialist (Most Common)

```
CLAUDE.md = Agent System Prompt
.claude/commands/review.md = Code Review Prompt
.claude/commands/security.md = Security Audit Prompt
.claude/commands/test.md = Testing Strategies Prompt
```

Use the base prompt for general work and specialist prompts as slash commands for specific tasks.

### Pattern 3: Layered (Team Projects)

```
Root CLAUDE.md = Agent System + Team Standards
src/CLAUDE.md = Architecture + conventions
src/api/CLAUDE.md = API-specific patterns
src/web/CLAUDE.md = Frontend-specific patterns
```

Each layer adds context without repeating information from parent levels.

### Pattern 4: Monorepo (Large Projects)

```
Root CLAUDE.md = Architecture overview + global rules
packages/ui/CLAUDE.md = Design system conventions
apps/web/CLAUDE.md = Web app conventions
apps/api/CLAUDE.md = API conventions
```

See the [Monorepo & Complex Projects prompt](../agents/monorepo-complex-projects-prompt.md) for detailed guidance.

---

## Getting the Most Value

### High-Impact Combinations

| Goal | Combination | Why It Works |
|------|------------|--------------|
| **Ship faster** | Agent System + Full-Stack Development | End-to-end patterns reduce decision fatigue |
| **Fewer bugs** | Agent System + Testing + Error Handling | Comprehensive quality gates |
| **Better security** | Agent System + Security Audit + Compliance | Layered security approach |
| **Team consistency** | Agent System + Code Review + DX & Tooling | Automated standards enforcement |
| **Scalable systems** | Agent System + Architecture + Cloud & Infra | Design + deployment in one workflow |
| **Production reliability** | Agent System + Monitoring + Error Handling | Full observability + resilience |

### Token Budget Optimization

When you have a limited token budget:

```
Priority 1 (< 2K tokens): Quick Reference only
Priority 2 (2K-4K tokens): Agent System prompt
Priority 3 (4K-8K tokens): Agent System + ONE specialist
Priority 4 (8K+ tokens): Agent System + specialist + project-type
```

**Tips to save tokens:**
- Put persistent context in CLAUDE.md (loaded automatically, doesn't consume message tokens)
- Use `/compact` mode for simple tasks
- Use `/clear` between unrelated tasks
- Put specialist prompts in `.claude/commands/` instead of CLAUDE.md (loaded only when needed)

---

## Measuring Prompt Effectiveness

### Track These Metrics

| Metric | How to Measure | Target |
|--------|---------------|--------|
| **First-attempt success rate** | How often does Claude's first response solve the task? | > 80% |
| **Iteration count** | How many back-and-forth messages per task? | < 3 for standard tasks |
| **Error rate** | How often does Claude introduce bugs? | < 5% |
| **Convention adherence** | Does output match your coding standards? | > 95% |
| **Context accuracy** | Does Claude understand your project correctly? | > 90% |

### Signs Your Prompts Need Updating

```markdown
❌ Claude keeps asking about your stack → Add to CLAUDE.md
❌ Claude uses wrong patterns → Add explicit "do" and "don't" lists
❌ Claude misses edge cases → Add relevant examples to prompt
❌ Claude ignores conventions → Move conventions to CLAUDE.md (always loaded)
❌ Claude generates verbose output → Add output format preferences
❌ Reviews miss security issues → Add Security Audit prompt
```

### Continuous Improvement Loop

```
1. USE prompts for a sprint/week
2. COLLECT feedback from team (what worked, what didn't)
3. IDENTIFY patterns in failures
4. UPDATE prompts to address gaps
5. SHARE changes with team
6. REPEAT
```

---

## Common Customizations

### By Programming Language

<details>
<summary><strong>TypeScript/JavaScript</strong></summary>

Add to your CLAUDE.md:
```markdown
## TypeScript Standards
- Strict mode enabled
- No `any` types (use `unknown` + type guards)
- Prefer `interface` over `type` for object shapes
- Use `as const` for literal types
- Zod for runtime validation
- Path aliases: `@/` → `src/`
```
</details>

<details>
<summary><strong>Python</strong></summary>

Add to your CLAUDE.md:
```markdown
## Python Standards
- Python 3.12+
- Type hints on all functions
- Pydantic for data validation
- Ruff for linting + formatting
- pytest for testing (not unittest)
- Async with asyncio (not threading)
```
</details>

<details>
<summary><strong>Go</strong></summary>

Add to your CLAUDE.md:
```markdown
## Go Standards
- Go 1.22+
- Standard library preferred over third-party
- Table-driven tests
- Errors as values (no panic in library code)
- golangci-lint for linting
- Context propagation in all functions
```
</details>

<details>
<summary><strong>Rust</strong></summary>

Add to your CLAUDE.md:
```markdown
## Rust Standards
- Latest stable Rust
- clippy for linting (deny warnings)
- thiserror for library errors, anyhow for applications
- serde for serialization
- tokio for async runtime
- proptest for property-based testing
```
</details>

### By Framework

| Framework | Key Additions to CLAUDE.md |
|-----------|---------------------------|
| **Next.js** | App Router vs Pages, Server Components, Server Actions |
| **NestJS** | Modules, providers, guards, interceptors, pipes |
| **Django** | Models, views, serializers, URL patterns |
| **FastAPI** | Pydantic models, dependency injection, async endpoints |
| **Spring Boot** | Annotations, beans, profiles, actuator |
| **Rails** | Convention over configuration, generators, concerns |

---

## Troubleshooting Prompt Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Claude ignores parts of the prompt | Prompt too long, key info buried | Move critical rules to the top of CLAUDE.md |
| Inconsistent coding style | No explicit style guide | Add formatter config + examples |
| Wrong architecture decisions | Missing project context | Add architecture overview to CLAUDE.md |
| Too verbose responses | No output format specified | Add "prefer concise responses" to prompt |
| Misses security issues | Only using base prompt | Add Security Audit prompt |
| Doesn't run tests | No test commands specified | Add build/test commands to CLAUDE.md |
| Creates wrong file structure | No structure documented | Add project structure diagram |

---

## Remember

```
✦ START SIMPLE: Begin with Agent System prompt, add specialists as needed
✦ CLAUDE.MD IS KEY: Persistent context that's always loaded — put critical info there
✦ TEAM STANDARDS: Append your conventions to any prompt — they will be followed
✦ MEASURE & ITERATE: Track effectiveness and update prompts based on real usage
✦ COMMANDS FOR SPECIALISTS: Put specialist prompts in .claude/commands/ to save tokens
✦ LAYER, DON'T REPEAT: Each CLAUDE.md level adds context, never duplicates
✦ CUSTOMIZE BY STACK: Add language and framework-specific conventions
✦ KEEP EVOLVING: Prompts should grow with your project — update them regularly
```
