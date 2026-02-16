# Quick Start

## 1. Pick Your Prompt

### AI Agents (Claude Code, Copilot, etc.)

| Task | Prompt | File |
|------|--------|------|
| Any autonomous task | **Agent System** ⭐ | [View](prompts/english/agents/claude-agent-system-prompt.md) |
| Debugging | Agent System + **Error Analysis** | [View](prompts/english/agents/error-analysis-prompt.md) |
| New/existing project | Agent System + **Project Workflow** | [View](prompts/english/agents/project-workflow-prompt.md) |
| PR review | Agent System + **Code Review** | [View](prompts/english/agents/code-review-prompt.md) |
| Security check | Agent System + **Security Audit** | [View](prompts/english/agents/security-audit-prompt.md) |
| Code improvement | Agent System + **Refactoring** | [View](prompts/english/agents/refactoring-prompt.md) |
| Test design | Agent System + **Testing** | [View](prompts/english/agents/testing-strategies-prompt.md) |
| Minimal context | **Quick Reference** only | [View](prompts/english/agents/agent-quick-reference.md) |

### Interactive Sessions

| Project | Prompts | Files |
|---------|---------|-------|
| Any project | **Foundation** ⭐ | [View](prompts/english/base/claude-foundation-prompt.md) |
| React / Vue app | Foundation + **Web Dev** | [View](prompts/english/project-types/web-development-prompt.md) |
| REST / GraphQL API | Foundation + **API Dev** | [View](prompts/english/project-types/api-development-prompt.md) |
| ML / Data Science | Foundation + **Data Science** | [View](prompts/english/project-types/data-science-ml-prompt.md) |
| iOS / Android app | Foundation + **Mobile** | [View](prompts/english/project-types/mobile-development-prompt.md) |
| DevOps / Infra | Foundation + **DevOps** | [View](prompts/english/project-types/devops-cicd-prompt.md) |
| Database design | Foundation + **Database** | [View](prompts/english/project-types/database-sql-prompt.md) |
| Full-stack app | Foundation + Web + API | — |

### Türkçe

| Prompt | Dosya |
|--------|-------|
| Agent Sistem | [View](prompts/turkish/agents/claude-agent-system-prompt-tr.md) |
| Temel Prompt | [View](prompts/turkish/base/claude-foundation-prompt-tr.md) |
| Kod İnceleme | [View](prompts/turkish/agents/code-review-prompt-tr.md) |
| Hata Analizi | [View](prompts/turkish/agents/error-analysis-prompt-tr.md) |

---

## 2. Copy & Paste

**Agent mode:** Copy the prompt file content → paste as system prompt → give your task.

**Interactive mode:** Copy Foundation + project prompt → paste at session start → describe your task.

---

## 3. Core Method (APEI)

```
ANALYZE → PLAN → EXECUTE → ITERATE
   ↑                          │
   └── Not optimal? ──────────┘
```

All prompts follow this cycle automatically.

---

## Token Budget

| Budget | Setup |
|--------|-------|
| < 2K | Quick Reference only |
| 2K–8K | Agent System Prompt |
| 8K+ | Agent System + project-type prompt |

---

## Documentation

- [README.md](README.md) — Full catalog & overview
- [USAGE.md](USAGE.md) — Detailed examples
- [Agent Index](prompts/english/agents/INDEX.md) — All agent prompts
- [English Index](prompts/english/INDEX.md) — All English prompts
- [Türkçe Index](prompts/turkish/INDEX.md) — Turkish prompts
- [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) — APEI deep-dive
