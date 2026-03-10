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
| Technical writing | Agent System + **Documentation** | [View](prompts/english/agents/documentation-prompt.md) |
| Optimize performance | Agent System + **Performance** | [View](prompts/english/agents/performance-optimization-prompt.md) |
| Git workflow | Agent System + **Git & VCS** | [View](prompts/english/agents/git-version-control-prompt.md) |
| System integrity | Agent System + **Integration Guardian** | [View](prompts/english/agents/integration-guardian-prompt.md) |
| Accessibility check | Agent System + **Accessibility Audit** | [View](prompts/english/agents/accessibility-audit-prompt.md) |
| Migration/upgrade | Agent System + **Migration & Upgrade** | [View](prompts/english/agents/migration-upgrade-prompt.md) |
| Set up monitoring | Agent System + **Monitoring & Observability** | [View](prompts/english/agents/monitoring-observability-prompt.md) |
| Minimal context | **Quick Reference** only | [View](prompts/english/agents/agent-quick-reference.md) |

### Claude Code-Specific

| Task | Prompt | File |
|------|--------|------|
| Mode planning (/think, /ultrathink) | **Claude Code Modes** ⭐ | [View](prompts/english/agents/claude-code-modes-prompt.md) |
| Token efficiency | **Claude Code Tokens** | [View](prompts/english/agents/claude-code-token-optimization-prompt.md) |
| CLAUDE.md & hooks setup | **Claude Code Workflow** | [View](prompts/english/agents/claude-code-workflow-prompt.md) |

### Architecture & Development

| Task | Prompt | File |
|------|--------|------|
| Tool/library selection | **Technology Stack** ⭐ | [View](prompts/english/agents/technology-stack-prompt.md) |
| System design & patterns | **Architecture Patterns** | [View](prompts/english/agents/architecture-patterns-prompt.md) |
| Modern full-stack app | **Full-Stack Development** | [View](prompts/english/agents/fullstack-development-prompt.md) |
| Complex multi-step tasks | **Prompt Chaining** | [View](prompts/english/agents/prompt-chaining-prompt.md) |
| Add AI/LLM features | **AI & LLM Integration** | [View](prompts/english/agents/ai-llm-integration-prompt.md) |

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
| General software | Foundation + **General Software** | [View](prompts/english/project-types/general-software-development-prompt.md) |
| Game development | Foundation + **Game Dev** | [View](prompts/english/project-types/game-development-prompt.md) |
| Embedded / IoT | Foundation + **Embedded & IoT** | [View](prompts/english/project-types/embedded-iot-prompt.md) |
| Full-stack app | Foundation + Web + API | — |

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
- [CHANGELOG.md](CHANGELOG.md) — Version history
- [CLAUDE.md](CLAUDE.md) — AI agent configuration for this repo
- [Agent Index](prompts/english/agents/INDEX.md) — All agent prompts
- [Prompt Index](prompts/english/INDEX.md) — All prompts by category
- [Prompt Selector](prompts/english/workflows/prompt-selector-guide.md) — Decision tree for choosing prompts
- [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) — APEI deep-dive
