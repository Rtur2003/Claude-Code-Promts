# Claude Code Setup & Integration Guide

> **Complete `.claude/` Configuration** | **Prompt Placement Strategies** | **Complex Project Structures**

## Overview

This guide covers everything you need to integrate prompts from this repository into your Claude Code environment. From single-project setups to enterprise monorepos with multiple agents, you'll learn exactly where each file goes and why.

---

## Understanding Claude Code's Configuration System

Claude Code uses a layered configuration system that reads from multiple sources in order of priority:

```
Priority (highest → lowest):
┌──────────────────────────────────────────────────────┐
│ 1. Conversation context (current session)            │
│ 2. Directory-level CLAUDE.md (nearest to file)       │
│ 3. Project-root CLAUDE.md                            │
│ 4. ~/.claude/CLAUDE.md (user-global)                 │
│ 5. .claude/settings.json (project settings)          │
│ 6. ~/.claude/settings.json (user-global settings)    │
└──────────────────────────────────────────────────────┘
```

---

## Core File Structure

### Minimal Setup (Single Project)

```
your-project/
├── CLAUDE.md                  # Project memory & conventions
├── .claude/
│   └── settings.json          # Hooks, permissions, MCP servers
└── src/
    └── ...
```

### Standard Setup (Growing Project)

```
your-project/
├── CLAUDE.md                  # Global project context
├── .claude/
│   ├── settings.json          # Hooks, permissions, MCP
│   └── commands/              # Custom slash commands
│       ├── review.md          # /project:review
│       ├── deploy.md          # /project:deploy
│       └── debug.md           # /project:debug
├── src/
│   └── CLAUDE.md              # Source-specific conventions
├── tests/
│   └── CLAUDE.md              # Testing conventions
└── docs/
    └── CLAUDE.md              # Documentation conventions
```

### Enterprise Setup (Monorepo / Multi-Service)

```
monorepo/
├── CLAUDE.md                  # Global: shared conventions, architecture overview
├── .claude/
│   ├── settings.json          # Global hooks and permissions
│   └── commands/
│       ├── review.md          # Cross-package review command
│       ├── test-all.md        # Run all tests across packages
│       └── deploy.md          # Deployment orchestration
├── packages/
│   ├── web/
│   │   ├── CLAUDE.md          # Frontend conventions (React, Next.js)
│   │   └── src/
│   │       ├── components/
│   │       │   └── CLAUDE.md  # Component patterns, naming
│   │       └── hooks/
│   │           └── CLAUDE.md  # Custom hook conventions
│   ├── api/
│   │   ├── CLAUDE.md          # Backend conventions (Node/Go/Python)
│   │   └── src/
│   │       ├── routes/
│   │       │   └── CLAUDE.md  # API route patterns
│   │       └── services/
│   │           └── CLAUDE.md  # Service layer patterns
│   ├── shared/
│   │   └── CLAUDE.md          # Shared library conventions
│   └── mobile/
│       └── CLAUDE.md          # Mobile-specific conventions
├── infrastructure/
│   └── CLAUDE.md              # IaC conventions (Terraform, K8s)
└── scripts/
    └── CLAUDE.md              # Build/deploy script conventions
```

---

## CLAUDE.md: Project Memory File

### What Goes in CLAUDE.md

CLAUDE.md is the single most important file for Claude Code. It persists across sessions, loads automatically, and provides context without consuming conversation tokens.

### Root CLAUDE.md Template

Use this as your project root `CLAUDE.md`. Copy and customize:

```markdown
# CLAUDE.md

## Project Overview
- Name: [Your Project Name]
- Type: [web app / API / CLI / library / monorepo]
- Stack: [primary language, framework, key dependencies]
- Repository structure: [brief description]

## Build & Development
- Install: `[install command]`
- Dev: `[dev server command]`
- Build: `[build command]`
- Test: `[test command]`
- Test single: `[single test command pattern]`
- Lint: `[lint command]`
- Format: `[format command]`
- Type check: `[type check command]`

## Code Conventions
- Style guide: [ESLint config / Prettier / team rules]
- Naming: [camelCase for vars, PascalCase for components, etc.]
- File naming: [kebab-case.ts / PascalCase.tsx / snake_case.py]
- Imports: [absolute paths / barrel files / path aliases]
- Tests: [co-located / separate directory / naming pattern]
- Commits: [conventional commits / custom format]

## Architecture
- Pattern: [MVC / Clean Architecture / Hexagonal / DDD]
- State management: [Redux / Zustand / Context / Pinia]
- API layer: [REST / GraphQL / tRPC / gRPC]
- Database: [PostgreSQL / MongoDB / SQLite]
- Auth: [JWT / OAuth / Session]

## Important Paths
- Source: src/
- Tests: tests/ or src/**/*.test.ts
- Config: config/
- API routes: src/routes/ or src/app/api/
- Components: src/components/
- Database: prisma/ or src/db/

## Common Tasks
- Add a new feature: [steps specific to your project]
- Add a new API endpoint: [steps]
- Add a new component: [steps]
- Run database migration: [command]
- Deploy: [deployment steps]

## Things to Avoid
- Don't modify [critical files] without team discussion
- Don't use [deprecated patterns]
- Don't commit [file types to exclude]
- Don't install packages without checking for alternatives already in use
- Don't bypass TypeScript with `any` type

## Current Focus
- [Current sprint/milestone goals]
- [Active feature branches and their purpose]
```

### Subdirectory CLAUDE.md Examples

#### `src/CLAUDE.md` (Source Code)

```markdown
# Source Code Conventions

## File Organization
- Group by feature, not by type
- Each feature directory: index.ts, types.ts, *.test.ts
- Shared utilities in src/lib/

## Patterns
- Use dependency injection for services
- Prefer composition over inheritance
- All async operations must handle errors explicitly
- Use Result<T, E> pattern instead of throwing

## Naming
- Interfaces: prefix with I (IUserRepository)
- Types: suffix with Type only if ambiguous
- Constants: UPPER_SNAKE_CASE
- Enums: PascalCase members
```

#### `tests/CLAUDE.md` (Testing)

```markdown
# Testing Conventions

## Structure
- Mirror source directory structure
- One test file per source module
- Use descriptive test names: "should [expected behavior] when [condition]"

## Patterns
- Arrange-Act-Assert (AAA) pattern
- Use factories for test data (tests/factories/)
- Mock external services, never the module under test
- Integration tests in tests/integration/
- E2E tests in tests/e2e/

## Commands
- Run all: `npm test`
- Run single: `npm test -- --testPathPattern="auth"`
- Run with coverage: `npm test -- --coverage`
- Watch mode: `npm test -- --watch`
```

#### `packages/api/CLAUDE.md` (Monorepo Package)

```markdown
# API Package

## Overview
Express/Fastify API server for the main application.

## Stack
- Runtime: Node.js 20+
- Framework: Fastify 4
- ORM: Drizzle
- Validation: Zod
- Auth: JWT with refresh tokens

## Commands (run from this directory)
- Dev: `pnpm dev`
- Test: `pnpm test`
- Build: `pnpm build`
- Migrate: `pnpm db:migrate`
- Seed: `pnpm db:seed`

## Conventions
- Route files export a Fastify plugin
- Business logic in services/, not routes/
- Use Zod schemas for request/response validation
- Shared types imported from @monorepo/shared
- All database queries through repository pattern
```

---

## .claude/settings.json: Project Configuration

### Complete Settings Schema

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Write",
      "Edit",
      "Bash(npm test)",
      "Bash(npm run lint)",
      "Bash(npm run build)",
      "Bash(npx tsc --noEmit)",
      "Bash(npx prettier --write *)"
    ],
    "deny": [
      "Bash(rm -rf /)",
      "Bash(curl *)",
      "Bash(wget *)"
    ]
  },
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "command": "if echo \"$CLAUDE_FILE_PATH\" | grep -qE '\\.(env|pem|key|secret)$'; then echo 'BLOCKED: sensitive file'; exit 1; fi"
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "command": "npx prettier --write \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
      },
      {
        "matcher": "Edit|Write",
        "command": "npx eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
      }
    ],
    "Notification": [
      {
        "matcher": "",
        "command": "echo \"[$(date)] Claude notification\" >> .claude/notifications.log"
      }
    ]
  },
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": ""
      }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/dir"]
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": ""
      }
    }
  }
}
```

### Hook Environment Variables

| Variable | Description | Available In |
|----------|-------------|-------------|
| `$CLAUDE_FILE_PATH` | Path of file being edited | PreToolUse, PostToolUse |
| `$CLAUDE_TOOL_NAME` | Name of the tool being used | PreToolUse, PostToolUse |

### Settings Hierarchy

```
~/.claude/settings.json          → User-global (applies to all projects)
your-project/.claude/settings.json → Project-level (committed to git)
```

Project settings override user-global settings. **Commit project settings to git** so the whole team shares the same configuration.

---

## .claude/commands/: Custom Slash Commands

### How Custom Commands Work

Files in `.claude/commands/` become available as slash commands in Claude Code. The filename becomes the command name.

```
.claude/commands/
├── review.md          → /project:review
├── deploy.md          → /project:deploy
├── debug.md           → /project:debug
├── new-feature.md     → /project:new-feature
└── security-check.md  → /project:security-check
```

### Command File Format

Each `.md` file contains the prompt that runs when the command is invoked. You can use `$ARGUMENTS` to accept parameters.

#### Example: `.claude/commands/review.md`

```markdown
Review the code changes in this project with these criteria:

1. **Correctness**: Does the code do what it's supposed to?
2. **Security**: Any injection, auth, or data exposure risks?
3. **Performance**: Any N+1 queries, memory leaks, or unnecessary computation?
4. **Tests**: Are new paths tested? Are edge cases covered?
5. **Style**: Does it follow our conventions in CLAUDE.md?

Focus on: $ARGUMENTS

Provide actionable feedback with specific file:line references.
```

Usage: `/project:review the authentication middleware changes`

#### Example: `.claude/commands/new-feature.md`

```markdown
Implement a new feature following our project's APEI cycle:

Feature: $ARGUMENTS

## Step 1: Analyze
- Read CLAUDE.md for project conventions
- Identify affected files and dependencies
- Check existing patterns for similar features

## Step 2: Plan
- Create a numbered implementation checklist
- Identify test cases needed
- List files to create/modify

## Step 3: Execute
- Implement step by step
- Add tests after each component
- Follow conventions from CLAUDE.md

## Step 4: Verify
- Run full test suite
- Run linter and type checker
- Verify the feature works end-to-end
```

Usage: `/project:new-feature user profile image upload with S3 storage`

#### Example: `.claude/commands/debug.md`

```markdown
Debug the following issue systematically:

Issue: $ARGUMENTS

## Protocol
1. **Reproduce**: Find the exact steps to trigger the bug
2. **Isolate**: Narrow down to the specific file and function
3. **Root cause**: Use /think mode to analyze deeply
4. **Fix**: Apply the minimal fix
5. **Verify**: Write a regression test
6. **Document**: Note the fix in the commit message

Use the project's test suite to verify the fix doesn't break anything.
```

Usage: `/project:debug login fails when email contains a plus sign`

---

## Placing Prompts from This Repository

### Strategy 1: Single Prompt in CLAUDE.md (Simple Projects)

For small projects, embed the core prompt directly in your `CLAUDE.md`:

```markdown
# CLAUDE.md

## System Prompt
[Paste the content of claude-agent-system-prompt.md here]

## Project Overview
[Your project-specific context]

## Build & Development
[Your project-specific commands]
```

### Strategy 2: Custom Commands (Task-Specific Prompts)

For projects needing multiple prompt types, use custom commands:

```
.claude/commands/
├── review.md          ← Content from code-review-prompt.md
├── security.md        ← Content from security-audit-prompt.md
├── refactor.md        ← Content from refactoring-prompt.md
├── test.md            ← Content from testing-strategies-prompt.md
├── debug.md           ← Content from debugging-troubleshooting-prompt.md
└── optimize.md        ← Content from performance-optimization-prompt.md
```

This way, you invoke each prompt as a slash command when needed, keeping token usage efficient.

### Strategy 3: Layered CLAUDE.md (Complex Projects)

For complex projects, distribute prompt content across CLAUDE.md files:

```
project/
├── CLAUDE.md                     ← Agent System Prompt + project overview
├── src/
│   ├── CLAUDE.md                 ← Code conventions from Foundation Prompt
│   ├── components/
│   │   └── CLAUDE.md             ← Web Development prompt patterns
│   └── api/
│       └── CLAUDE.md             ← API Development prompt patterns
├── tests/
│   └── CLAUDE.md                 ← Testing Strategies prompt patterns
├── infrastructure/
│   └── CLAUDE.md                 ← Cloud & Infrastructure prompt patterns
└── .claude/
    └── commands/                 ← Task-specific prompts as commands
```

### Strategy 4: Team Shared Configuration (Team Projects)

For teams, create a shared prompt repository and reference it:

```
your-org/
├── claude-prompts/               ← Fork of this repo, customized
│   └── team/
│       ├── code-review.md        ← Team-specific review standards
│       ├── security.md           ← Company security requirements
│       └── onboarding.md         ← New developer setup
└── your-project/
    ├── CLAUDE.md                 ← References team standards
    └── .claude/
        └── commands/             ← Symlink or copy from claude-prompts/
```

---

## Complex Scenario: Multi-Prompt Composition

### When You Need Multiple Prompts at Once

Some tasks require combining prompts. Here's how to compose them effectively:

#### Scenario: Full-Stack Feature (Frontend + Backend + Database)

**CLAUDE.md** approach — add a task-specific section:

```markdown
# CLAUDE.md

## Current Task Context
This task involves full-stack changes. Follow these combined guidelines:

### Frontend (from Web Development prompt)
- Use React Server Components by default
- Client components only for interactivity
- Validate with Zod on both client and server

### Backend (from API Development prompt)
- RESTful endpoints with proper status codes
- Idempotency keys for mutations
- Rate limiting on public endpoints

### Database (from Database prompt)
- Migrations are forward-only
- Index all foreign keys
- Use transactions for multi-table operations
```

#### Scenario: Security-Critical Release

Create a compound command:

```markdown
<!-- .claude/commands/secure-release.md -->
Perform a security-focused release review combining:

## Security Audit (from security-audit-prompt)
- Check OWASP Top 10
- Review authentication flows
- Scan for hardcoded secrets
- Check dependency vulnerabilities

## Compliance Check (from compliance-governance-prompt)
- Verify data handling meets GDPR requirements
- Check PII exposure in logs
- Validate consent flows

## Performance Baseline (from performance-optimization-prompt)
- Measure response times for critical paths
- Check for memory leaks under load
- Verify CDN caching headers

Target: $ARGUMENTS
```

#### Scenario: Legacy Migration

```markdown
<!-- .claude/commands/migrate.md -->
Orchestrate a migration using combined strategies:

## Step 1: Audit (Architecture Patterns prompt)
- Map current architecture
- Identify coupling points
- Document data flows

## Step 2: Plan (Migration & Upgrade prompt)
- Order changes by dependency
- Plan rollback at each step
- Set up feature flags

## Step 3: Execute (Refactoring prompt)
- Apply strangler fig pattern
- Refactor in small, testable steps
- Maintain backward compatibility

## Step 4: Validate (Testing Strategies prompt)
- Run contract tests
- Verify integration points
- Load test critical paths

Migration target: $ARGUMENTS
```

---

## Prompt Composition Conflict Matrix

When combining multiple prompts, be aware of potential conflicts:

| Combination | Potential Conflict | Resolution |
|-------------|-------------------|------------|
| Security + Performance | Security may add overhead | Prioritize security; optimize within constraints |
| Refactoring + Testing | Refactoring may break tests | Update tests alongside refactoring; never skip |
| Architecture + Migration | New arch patterns vs. legacy constraints | Incremental migration; don't rewrite everything |
| Full-Stack + Token Optimization | Full-stack needs detailed context | Use directory-level CLAUDE.md to scope context |
| Code Review + Compact Mode | Review needs depth; compact saves tokens | Use /think for review, /compact for applying fixes |

---

## User-Global Configuration

### ~/.claude/CLAUDE.md (Personal Defaults)

Set your personal coding preferences that apply to all projects:

```markdown
# Personal Claude Code Preferences

## My Defaults
- Prefer TypeScript over JavaScript
- Use functional programming patterns when possible
- Always add JSDoc for public APIs
- I prefer explicit error handling over try/catch

## Communication
- Be concise, skip obvious explanations
- Show code diffs, not full file rewrites
- Ask before making large refactors

## My Workflow
- I use Git Flow branching
- I prefer squash merges
- I want conventional commit messages
```

### ~/.claude/settings.json (Personal Tool Settings)

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Edit",
      "Write"
    ]
  },
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-token"
      }
    }
  }
}
```

---

## Real-World Setup Examples

### Example 1: Solo Developer — Next.js SaaS

```
my-saas/
├── CLAUDE.md                          # Stack: Next.js 14, Prisma, Stripe
├── .claude/
│   ├── settings.json                  # Auto-format, auto-lint hooks
│   └── commands/
│       ├── new-page.md                # Template for new pages
│       ├── new-api.md                 # Template for API routes
│       └── deploy.md                  # Deployment checklist
├── src/
│   ├── CLAUDE.md                      # Component patterns, data fetching
│   └── ...
└── prisma/
    └── CLAUDE.md                      # Schema conventions, migration steps
```

### Example 2: Team of 5 — Microservices

```
platform/
├── CLAUDE.md                          # Architecture overview, shared conventions
├── .claude/
│   ├── settings.json                  # Shared hooks for all services
│   └── commands/
│       ├── review.md                  # Team code review standards
│       ├── new-service.md             # Service scaffolding template
│       └── incident.md               # Incident response checklist
├── services/
│   ├── auth-service/
│   │   ├── CLAUDE.md                  # Auth patterns, token management
│   │   └── ...
│   ├── payment-service/
│   │   ├── CLAUDE.md                  # Payment flow, idempotency rules
│   │   └── ...
│   └── notification-service/
│       ├── CLAUDE.md                  # Queue patterns, retry logic
│       └── ...
├── shared/
│   └── CLAUDE.md                      # Shared types, utilities, contracts
└── infrastructure/
    └── CLAUDE.md                      # Terraform modules, K8s manifests
```

### Example 3: Enterprise — Multi-Team Monorepo

```
enterprise-mono/
├── CLAUDE.md                          # Org-wide: architecture principles, ADRs
├── .claude/
│   ├── settings.json                  # Enterprise hooks (security, compliance)
│   └── commands/
│       ├── security-check.md          # Company security audit protocol
│       ├── compliance-review.md       # GDPR/SOC2 compliance check
│       ├── onboard-dev.md             # New developer setup
│       └── adr.md                     # Create Architecture Decision Record
├── apps/
│   ├── customer-portal/
│   │   ├── CLAUDE.md                  # Customer-facing app conventions
│   │   └── .claude/
│   │       └── commands/
│   │           └── a11y-check.md      # Accessibility audit for this app
│   ├── admin-dashboard/
│   │   └── CLAUDE.md
│   └── mobile-app/
│       └── CLAUDE.md
├── libs/
│   ├── ui-components/
│   │   └── CLAUDE.md                  # Design system patterns
│   ├── api-client/
│   │   └── CLAUDE.md
│   └── auth/
│       └── CLAUDE.md
├── services/
│   └── [same as microservices above]
└── tools/
    └── CLAUDE.md                      # Internal tooling conventions
```

---

## Multi-Session Workflow Patterns

### Pattern 1: Deep Work Sessions

```
Session 1: Architecture (with /think or /ultrathink)
├── Read CLAUDE.md for context
├── Design solution architecture
├── Document decisions in CLAUDE.md
└── Create implementation plan

/clear → Reset context

Session 2: Implementation (Normal mode)
├── CLAUDE.md auto-loads previous decisions
├── Execute plan step by step
├── Run tests after each step
└── Update CLAUDE.md with progress

/clear → Reset context

Session 3: Review & Polish (Mixed modes)
├── /think → Code review
├── Normal → Apply fixes
├── /compact → Final cleanup
└── Update CLAUDE.md with learnings
```

### Pattern 2: Parallel Workstreams

When working on multiple features simultaneously:

```
CLAUDE.md tracks:
## Active Workstreams
### Feature A (branch: feat/user-profiles)
- Status: Step 3/5 — implementing profile API
- Last session: designed database schema
- Next: implement CRUD endpoints

### Feature B (branch: feat/notifications)
- Status: Step 1/4 — analyzing requirements
- Next: design notification data model

### Bug Fix (branch: fix/auth-race)
- Status: Identified root cause
- Next: implement fix and regression test
```

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|---------|
| CLAUDE.md not being read | File not in project root | Move to repo root directory |
| Hooks not firing | Invalid JSON in settings.json | Validate JSON syntax |
| Custom command not showing | Wrong directory or extension | Must be `.claude/commands/*.md` |
| Context lost between sessions | CLAUDE.md not updated | Use `/memory` to save state |
| Too many tokens consumed | CLAUDE.md too large | Split into directory-level files |
| Team settings conflicting | Multiple settings sources | Use project `.claude/settings.json` |
| MCP server not connecting | Wrong command or env vars | Test server command manually |

---

## Checklist: Setting Up Your Project

- [ ] Create root `CLAUDE.md` with project overview and conventions
- [ ] Create `.claude/settings.json` with hooks and permissions
- [ ] Add `.claude/commands/` for task-specific prompts you use often
- [ ] Add subdirectory `CLAUDE.md` files for complex projects
- [ ] Commit `.claude/` directory to git for team sharing
- [ ] Add sensitive values (tokens, secrets) to `.gitignore` or use env vars
- [ ] Test hooks by making a small edit and verifying auto-format runs
- [ ] Test custom commands with `/project:command-name`
- [ ] Review token usage with `/cost` after first session

---

## Remember

> **Configuration is an investment. A well-configured Claude Code environment multiplies every session's productivity.**

Key principles:
1. **CLAUDE.md is your project's brain** — keep it accurate and up to date
2. **Hooks automate quality** — auto-format, auto-lint, block risky edits
3. **Custom commands are your shortcuts** — turn complex workflows into one-liners
4. **Layer your configuration** — global defaults + project specifics + directory context
5. **Commit your config** — team alignment through shared `.claude/` settings
6. **Update after every session** — CLAUDE.md should grow smarter with your project
