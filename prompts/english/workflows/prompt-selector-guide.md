# Prompt Selector Guide

Single source of truth for prompt selection. Keep decision logic here and reference this file from other catalogs.

---

## Decision Tree (Source of Truth)

```text
Start
 ├─ Need autonomous execution? → Agent System
 │   ├─ Token budget < 2K? → Quick Reference only
 │   └─ Need domain depth? → Add exactly one specialist prompt
 │       ├─ Debug/incident → Debugging & Troubleshooting
 │       ├─ Security/risk  → Security Audit
 │       ├─ Architecture   → Architecture Patterns
 │       ├─ Performance    → Performance Optimization
 │       ├─ Refactor       → Refactoring
 │       ├─ Migration      → Migration & Upgrade
 │       └─ Multi-agent    → Multi-Agent Orchestration
 └─ Need interactive collaboration? → Foundation + one project-type prompt
```

Rule: start minimal, add only if explicit success criteria are not met.

---

## Quick Scenario Mapping

| Scenario | Recommended Setup |
|----------|-------------------|
| General autonomous coding | Agent System |
| Production debugging | Agent System + Debugging & Troubleshooting |
| Security-sensitive task | Agent System + Security Audit |
| Architecture decisions | Agent System + Architecture Patterns |
| Complex parallel execution | Agent System + Multi-Agent Orchestration |
| Interactive web/API build | Foundation + Web/API project-type prompt |

---

## Token Budget

| Budget | Setup |
|--------|-------|
| < 2K | Quick Reference only |
| 2K–8K | Agent System |
| 8K+ | Agent System + exactly one specialist |

---

## Anti-Patterns

- Don’t stack many specialist prompts “just in case.”
- Don’t use archived prompts from `agents/archive/` in active setup.
- Don’t skip core prompts (`Agent System` for agent mode, `Foundation` for interactive mode).

---

## See Also

- [README.md](../../../README.md)
- [QUICK-START.md](../../../QUICK-START.md)
- [USAGE.md](../../../USAGE.md)
- [Agent Index](../agents/INDEX.md)
- [Prompt Index](../INDEX.md)
