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
| Claude Code, mode planning | Agent System + Claude Code Modes |
| Claude Code, token efficiency | Agent System + Claude Code Tokens |
| Claude Code, project setup | Agent System + Claude Code Workflow |
| Interactive, React app | Foundation + Web Development |
| Interactive, REST API | Foundation + API Development |
| Interactive, ML model | Foundation + Data Science & ML |
| Interactive, full-stack | Foundation + Web + API |
| Interactive, mobile | Foundation + Mobile Development |
| Interactive, infra | Foundation + DevOps & CI/CD |

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

**Evaluate:**
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

- [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) — APEI cycle deep-dive
- [Agent Index](prompts/english/agents/INDEX.md) — All agent prompts
- [Examples](prompts/english/examples/) — More real-world examples
