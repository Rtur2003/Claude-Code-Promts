# Usage Guide

## Getting Started

### 1. Identify Your Needs

| Question | Determines |
|----------|-----------|
| Using an AI coding agent? | → Agent prompts |
| Interactive Claude session? | → Foundation + project-type prompts |
| What tech stack? | → Which project-type prompt |
| Token budget? | → How many prompts to combine |

### 2. Select Prompts

| Scenario | Prompts |
|----------|---------|
| AI agent, any task | Agent System |
| AI agent, debugging | Agent System + Error Analysis |
| AI agent, project | Agent System + Project Workflow |
| AI agent, code review | Agent System + Code Review |
| AI agent, security | Agent System + Security Audit |
| AI agent, refactoring | Agent System + Refactoring |
| AI agent, testing | Agent System + Testing |
| AI agent, docs | Agent System + Documentation |
| AI agent, performance | Agent System + Performance |
| AI agent, git workflow | Agent System + Git & VCS |
| AI agent, integration | Agent System + Integration Guardian |
| AI agent, accessibility | Agent System + Accessibility Audit |
| AI agent, migration | Agent System + Migration & Upgrade |
| AI agent, monitoring | Agent System + Monitoring & Observability |
| AI agent, production debugging | Agent System + Debugging & Troubleshooting |
| AI agent, API design | Agent System + API Design & GraphQL |
| AI agent, cloud deploy | Agent System + Cloud & Infrastructure |
| AI agent, data pipelines | Agent System + Data Engineering |
| AI agent, compliance | Agent System + Compliance & Governance |
| AI agent, multi-agent | Agent System + Multi-Agent Orchestration |
| AI agent, monorepo | Agent System + Monorepo & Complex Projects |
| AI agent, error handling | Agent System + Error Handling & Resilience |
| AI agent, DX / tooling | Agent System + Developer Experience & Tooling |
| Claude Code, mode planning | Agent System + Claude Code Modes |
| Claude Code, token efficiency | Agent System + Claude Code Tokens |
| Claude Code, project setup | Agent System + Claude Code Workflow |
| Choose tools/libraries | Agent System + Technology Stack |
| System architecture | Agent System + Architecture Patterns |
| Full-stack development | Agent System + Full-Stack Development |
| AI/LLM integration | Agent System + AI & LLM Integration |
| Complex multi-step project | Agent System + Prompt Chaining |
| Interactive, React app | Foundation + Web Development |
| Interactive, REST API | Foundation + API Development |
| Interactive, ML model | Foundation + Data Science & ML |
| Interactive, full-stack | Foundation + Web + API |
| Interactive, mobile | Foundation + Mobile Development |
| Interactive, infra | Foundation + DevOps & CI/CD |
| Interactive, database | Foundation + Database & SQL |
| Interactive, general | Foundation + General Software |
| Interactive, game dev | Foundation + Game Development |
| Interactive, embedded/IoT | Foundation + Embedded & IoT |
| Interactive, blockchain | Foundation + Blockchain & Web3 |
| Interactive, desktop app | Foundation + Desktop Apps |

### 3. Apply

**Agent mode:**
```
[Paste agent prompt content as system prompt]
[Give your task]
→ Agent runs APEI cycle automatically
```

**Interactive mode:**
```
Please use this system prompt for our session:
[Paste Foundation + project-type prompt content]

I need to [describe your task].
Let's start with analysis.
```

---

## Example: JWT Authentication API

### Setup
```
Prompt: Foundation + API Development
Task: JWT authentication for Express API
Stack: Node.js, Express, PostgreSQL
```

### Iteration 1 — Basic Auth

**Analyze:** Express server running, PostgreSQL set up, User model exists, no auth yet.

**Plan:**
1. Install jsonwebtoken, bcrypt
2. Create password hashing utility
3. Create login endpoint + JWT generation
4. Create auth middleware
5. Add tests

**Execute:** Implement steps 1–5 with tests after each step.

**Iterate:**
- ✓ Login works, tokens generated, routes protected
- ⚠ No refresh tokens, short expiry

### Iteration 2 — Refresh Tokens

**Plan:** Add refresh token mechanism + database storage + optimize bcrypt rounds.

**Result:** Access token 15min, refresh 7 days, login 40% faster, 92% test coverage. **Done.**

---

## Example: React DataTable Component

### Setup
```
Prompt: Foundation + Web Development
Task: Reusable DataTable with sort, pagination, a11y
Stack: React 18, TypeScript, Tailwind
```

### Iteration 1 — Basic rendering + TypeScript types
### Iteration 2 — Add sorting (useMemo) + pagination
### Iteration 3 — Keyboard navigation, ARIA attributes, responsive overflow

**Result:** WCAG AA compliant, screen-reader compatible, Lighthouse a11y: 100. **Done.**

---

## Advanced: Combining Prompts

For full-stack applications:
```
System Context:
1. Foundation Prompt (core principles)
2. Web Development Prompt (frontend)
3. API Development Prompt (backend)
```

For team customization, append to any prompt:
```
## Team Standards
- Stack: Next.js 14, NestJS, PostgreSQL/Prisma, Jest + Playwright
- Conventions: Conventional commits, 80% coverage min, 2 PR approvals
```

---

## Troubleshooting

| Issue | Solution |
|-------|---------|
| Claude not following prompt | Reinforce: "Follow the APEI cycle from the system prompt" |
| Too many iterations | Set max: "Maximum 3 iterations. Success criteria: [list]" |
| Scope creep | Reset: "Focus only on [original goal]. Other improvements → separate task" |

---

## Next Steps

- [Prompt Selector](prompts/english/workflows/prompt-selector-guide.md) — Find the right prompt for your task
- [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) — APEI cycle deep-dive
- [Agent Index](prompts/english/agents/INDEX.md) — All agent prompts
- [Examples](prompts/english/examples/) — More real-world examples
