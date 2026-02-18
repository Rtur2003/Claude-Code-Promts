# Claude Code Prompts

Production-ready system prompts for Claude AI and coding agents. Built on the **APEI cycle**: Analyze → Plan → Execute → Iterate.

## Prompt Catalog

### 🤖 Agent Prompts (Autonomous AI Agents)

| Prompt | Purpose | Tokens | File |
|--------|---------|--------|------|
| **Agent System** ⭐ | Core operating system | ~1.5K | [View](prompts/english/agents/claude-agent-system-prompt.md) |
| **Error Analysis** | Debugging & root cause | ~2K | [View](prompts/english/agents/error-analysis-prompt.md) |
| **Project Workflow** | Full lifecycle management | ~2.5K | [View](prompts/english/agents/project-workflow-prompt.md) |
| **Quick Reference** | Cheat sheet (minimal) | ~0.8K | [View](prompts/english/agents/agent-quick-reference.md) |
| **Code Review** | Systematic PR review | ~2K | [View](prompts/english/agents/code-review-prompt.md) |
| **Security Audit** | Vulnerability detection | ~2.5K | [View](prompts/english/agents/security-audit-prompt.md) |
| **Refactoring** | Code improvement | ~2.5K | [View](prompts/english/agents/refactoring-prompt.md) |
| **Testing** | Test design & TDD | ~3K | [View](prompts/english/agents/testing-strategies-prompt.md) |
| **Documentation** | Technical writing | ~2.5K | [View](prompts/english/agents/documentation-prompt.md) |
| **Performance** | Optimization & profiling | ~3K | [View](prompts/english/agents/performance-optimization-prompt.md) |
| **Git & VCS** | Branching & commits | ~2.5K | [View](prompts/english/agents/git-version-control-prompt.md) |
| **Integration Guardian** | System integrity | ~0.5K | [View](prompts/english/agents/integration-guardian-prompt.md) |

### 🎯 Claude Code-Specific Prompts

| Prompt | Purpose | Tokens | File |
|--------|---------|--------|------|
| **Mode Transitions** ⭐ | /think, /ultrathink, /compact modes & planning | ~2.5K | [View](prompts/english/agents/claude-code-modes-prompt.md) |
| **Token Optimization** | Token saving strategies for Claude Code | ~2.5K | [View](prompts/english/agents/claude-code-token-optimization-prompt.md) |
| **Workflow & Config** | CLAUDE.md, hooks, permissions, MCP | ~3K | [View](prompts/english/agents/claude-code-workflow-prompt.md) |

### 📋 Foundation & Project Prompts (Interactive Sessions)

| Prompt | Purpose | Technologies | File |
|--------|---------|-------------|------|
| **Foundation** ⭐ | Universal best practices | Any | [View](prompts/english/base/claude-foundation-prompt.md) |
| **Web Development** | Frontend apps | React, Vue, Angular, CSS | [View](prompts/english/project-types/web-development-prompt.md) |
| **API Development** | Backend services | REST, GraphQL, Node, Go | [View](prompts/english/project-types/api-development-prompt.md) |
| **Data Science & ML** | ML pipelines | Python, pandas, PyTorch | [View](prompts/english/project-types/data-science-ml-prompt.md) |
| **Mobile** | Mobile apps | iOS, Android, Flutter, RN | [View](prompts/english/project-types/mobile-development-prompt.md) |
| **DevOps & CI/CD** | Infrastructure | K8s, Docker, Terraform | [View](prompts/english/project-types/devops-cicd-prompt.md) |
| **Database & SQL** | Data layer | PostgreSQL, MySQL, Redis | [View](prompts/english/project-types/database-sql-prompt.md) |
| **General Software** | Cross-language | Python, JS, Go, Java, C# | [View](prompts/english/project-types/general-software-development-prompt.md) |

### 🌍 Language Support

| Language | Status | Prompts | Link |
|----------|--------|---------|------|
| English | ✅ Complete | 15 agent + 8 project | [Index](prompts/english/INDEX.md) |
| Türkçe | 🔄 In Progress | 7 prompts | [Index](prompts/turkish/INDEX.md) |

---

## Quick Start

### For AI Agents (Claude Code, Copilot)

```
1. Copy content of claude-agent-system-prompt.md
2. Paste as system prompt
3. Give task → Agent runs APEI cycle automatically
```

### For Interactive Sessions

```
1. Copy Foundation prompt + project-type prompt
2. Paste at start of Claude session
3. Describe your task → Follow the APEI cycle together
```

### Token Budget Guide

| Context Budget | Recommended Setup |
|----------------|-------------------|
| < 2K tokens | Quick Reference only |
| 2K–8K tokens | Agent System Prompt |
| 8K+ tokens | Agent System + project-type prompt |

---

## Common Combinations

| Project Type | Prompts to Use |
|-------------|----------------|
| AI Agent Task | Agent System |
| Claude Code Setup | Agent System + Workflow & Config |
| Claude Code Planning | Agent System + Mode Transitions |
| Token-Efficient Session | Agent System + Token Optimization |
| Debug / Fix Bugs | Agent System + Error Analysis |
| New Project | Agent System + Project Workflow |
| Code Review | Agent System + Code Review |
| React / Vue App | Foundation + Web Development |
| REST API | Foundation + API Development |
| ML Model | Foundation + Data Science & ML |
| Mobile App | Foundation + Mobile |
| Full-Stack App | Foundation + Web + API |
| DevOps / Infra | Foundation + DevOps & CI/CD |

---

## Repository Structure

```
prompts/
├── english/
│   ├── agents/          # Agent-optimized prompts (15 files)
│   ├── base/            # Foundation prompt
│   ├── project-types/   # Domain-specific prompts (7 files)
│   ├── examples/        # Real-world usage examples
│   └── workflows/       # APEI methodology guide
├── turkish/
│   ├── agents/          # Türkçe agent prompts (6 files)
│   ├── base/            # Türkçe foundation prompt
│   └── INDEX.md
```

## Resources

| Resource | Description |
|----------|-------------|
| [QUICK-START.md](QUICK-START.md) | 30-second setup guide |
| [USAGE.md](USAGE.md) | Detailed examples & advanced usage |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution guidelines |
| [Agent Index](prompts/english/agents/INDEX.md) | Full agent prompt catalog |
| [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) | APEI methodology deep-dive |

## Customization

Fork → Modify prompts → Add team standards → Use.

All prompts are MIT-licensed templates. Adapt for your stack, conventions, and tools.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Key areas: new languages, new project types, prompt improvements, examples.

## License

MIT License — use, modify, and distribute freely.
