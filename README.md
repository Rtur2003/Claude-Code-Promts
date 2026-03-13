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
| **Security Audit** | Vulnerability detection + cloud security | ~3.5K | [View](prompts/english/agents/security-audit-prompt.md) |
| **Refactoring** | Code improvement | ~2.5K | [View](prompts/english/agents/refactoring-prompt.md) |
| **Testing** | Test design, TDD, chaos & contract testing | ~4K | [View](prompts/english/agents/testing-strategies-prompt.md) |
| **Documentation** | Technical writing | ~2.5K | [View](prompts/english/agents/documentation-prompt.md) |
| **Performance** | Optimization, profiling, CDN & edge | ~3.5K | [View](prompts/english/agents/performance-optimization-prompt.md) |
| **Git & VCS** | Branching & commits | ~2.5K | [View](prompts/english/agents/git-version-control-prompt.md) |
| **Integration Guardian** | System integrity | ~3.5K | [View](prompts/english/agents/integration-guardian-prompt.md) |
| **Accessibility Audit** | WCAG 2.2 compliance | ~3K | [View](prompts/english/agents/accessibility-audit-prompt.md) |
| **Migration & Upgrade** | Framework & DB migrations | ~2.5K | [View](prompts/english/agents/migration-upgrade-prompt.md) |
| **Monitoring & Observability** | Logs, metrics, traces | ~3K | [View](prompts/english/agents/monitoring-observability-prompt.md) |
| **Debugging & Troubleshooting** | Production debugging & incident response | ~3.5K | [View](prompts/english/agents/debugging-troubleshooting-prompt.md) |

### 🎯 Claude Code-Specific Prompts

| Prompt | Purpose | Tokens | File |
|--------|---------|--------|------|
| **Mode Transitions** ⭐ | /think, /ultrathink, /compact modes & planning | ~2.5K | [View](prompts/english/agents/claude-code-modes-prompt.md) |
| **Token Optimization** | Token saving strategies for Claude Code | ~2.5K | [View](prompts/english/agents/claude-code-token-optimization-prompt.md) |
| **Workflow & Config** | CLAUDE.md, hooks, permissions, MCP | ~3K | [View](prompts/english/agents/claude-code-workflow-prompt.md) |

### 🏗️ Architecture & Full-Stack Prompts

| Prompt | Purpose | Tokens | File |
|--------|---------|--------|------|
| **Technology Stack** ⭐ | Library discovery, modern tools, hidden gems | ~4K | [View](prompts/english/agents/technology-stack-prompt.md) |
| **Architecture Patterns** | System design, event sourcing, saga, serverless | ~4.5K | [View](prompts/english/agents/architecture-patterns-prompt.md) |
| **Full-Stack Development** | Next.js/Nuxt/SvelteKit, WebSocket, background jobs | ~4.5K | [View](prompts/english/agents/fullstack-development-prompt.md) |
| **Prompt Chaining** | Multi-step workflows, context management | ~3K | [View](prompts/english/agents/prompt-chaining-prompt.md) |
| **AI & LLM Integration** | RAG, vector DBs, AI agents, safety | ~3.5K | [View](prompts/english/agents/ai-llm-integration-prompt.md) |
| **API Design & GraphQL** | Schema-first, DataLoader, caching, contracts | ~4K | [View](prompts/english/agents/api-design-graphql-prompt.md) |
| **Cloud & Infrastructure** | IaC, multi-region, K8s, cost optimization | ~4K | [View](prompts/english/agents/cloud-infrastructure-prompt.md) |
| **Data Engineering** | Pipelines, dbt, streaming, data quality | ~4K | [View](prompts/english/agents/data-engineering-prompt.md) |
| **Compliance & Governance** | GDPR, HIPAA, SOC 2, threat modeling | ~3.5K | [View](prompts/english/agents/compliance-governance-prompt.md) |
| **Multi-Agent Orchestration** | Agent coordination, parallel execution, shared state | ~4K | [View](prompts/english/agents/multi-agent-orchestration-prompt.md) |
| **Monorepo & Complex Projects** | Multi-package architecture, cross-cutting concerns | ~4.5K | [View](prompts/english/agents/monorepo-complex-projects-prompt.md) |

### 📋 Foundation & Project Prompts (Interactive Sessions)

| Prompt | Purpose | Technologies | File |
|--------|---------|-------------|------|
| **Foundation** ⭐ | Universal best practices | Any | [View](prompts/english/base/claude-foundation-prompt.md) |
| **Web Development** | Frontend apps + SEO + a11y | React, Vue, Angular, CSS | [View](prompts/english/project-types/web-development-prompt.md) |
| **API Development** | Backend services + idempotency | REST, GraphQL, Node, Go | [View](prompts/english/project-types/api-development-prompt.md) |
| **Data Science & ML** | ML pipelines + MLOps | Python, pandas, PyTorch | [View](prompts/english/project-types/data-science-ml-prompt.md) |
| **Mobile** | Mobile apps | iOS, Android, Flutter, RN | [View](prompts/english/project-types/mobile-development-prompt.md) |
| **DevOps & CI/CD** | Infrastructure | K8s, Docker, Terraform | [View](prompts/english/project-types/devops-cicd-prompt.md) |
| **Database & SQL** | Data layer | PostgreSQL, MySQL, Redis | [View](prompts/english/project-types/database-sql-prompt.md) |
| **General Software** | Cross-language | Python, JS, Go, Java, C# | [View](prompts/english/project-types/general-software-development-prompt.md) |
| **Game Development** | Game engines | Unity, Unreal, Godot | [View](prompts/english/project-types/game-development-prompt.md) |
| **Embedded & IoT** | Hardware/firmware | C, C++, Rust, FreeRTOS | [View](prompts/english/project-types/embedded-iot-prompt.md) |
| **Blockchain & Web3** | Smart contracts & dApps | Solidity, Rust, Foundry | [View](prompts/english/project-types/blockchain-web3-prompt.md) |
| **Desktop Apps** | Cross-platform desktop | Tauri, Electron, Qt | [View](prompts/english/project-types/desktop-development-prompt.md) |

---

## Quick Start

### For Claude Code (Native Integration)

```
1. Create CLAUDE.md in your project root
2. Paste content from claude-agent-system-prompt.md into CLAUDE.md
3. Create .claude/commands/ for task-specific prompts
4. See the full setup guide: workflows/claude-code-setup-guide.md
```

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
| Debug / Fix Bugs | Agent System + Debugging & Troubleshooting |
| Production Incident | Agent System + Debugging + Monitoring |
| New Project | Agent System + Project Workflow |
| Choose Best Tools | Agent System + Technology Stack |
| System Architecture | Agent System + Architecture Patterns |
| Full-Stack App (modern) | Agent System + Full-Stack Development |
| API Design (GraphQL) | Agent System + API Design & GraphQL |
| Complex Multi-Step Task | Agent System + Prompt Chaining |
| Add AI/LLM Features | Agent System + AI & LLM Integration |
| Code Review | Agent System + Code Review |
| Security Check | Agent System + Security Audit |
| Compliance Audit | Agent System + Compliance & Governance |
| Accessibility Check | Agent System + Accessibility Audit |
| Reduce Tech Debt | Agent System + Refactoring |
| Framework/DB Migration | Agent System + Migration & Upgrade |
| Write Tests | Agent System + Testing |
| Write Docs | Agent System + Documentation |
| Optimize Speed | Agent System + Performance |
| Cloud Deployment | Agent System + Cloud & Infrastructure |
| Data Pipelines | Agent System + Data Engineering |
| Set Up Monitoring | Agent System + Monitoring & Observability |
| Git Workflow | Agent System + Git & VCS |
| Cross-Cutting Integrity | Agent System + Integration Guardian |
| Multi-Agent Teamwork | Agent System + Multi-Agent Orchestration |
| Monorepo Architecture | Agent System + Monorepo & Complex Projects |
| Full Claude Code Setup | Agent System + Workflow + Modes + Token Optimization |
| React / Vue App | Foundation + Web Development |
| REST API | Foundation + API Development |
| ML Model | Foundation + Data Science & ML |
| Mobile App | Foundation + Mobile |
| DevOps / Infra | Foundation + DevOps & CI/CD |
| Database Design | Foundation + Database & SQL |
| General Software | Foundation + General Software |
| Game Development | Foundation + Game Development |
| Embedded / IoT | Foundation + Embedded & IoT |
| Smart Contracts | Foundation + Blockchain & Web3 |
| Desktop App | Foundation + Desktop Apps |

---

## Repository Structure

```
prompts/
└── english/
    ├── agents/          # Agent-optimized prompts (30 files)
    ├── base/            # Foundation prompt
    ├── project-types/   # Domain-specific prompts (11 files)
    ├── examples/        # Real-world usage examples (7 files)
    └── workflows/       # APEI methodology, prompt selection, troubleshooting & setup guides
```

## Resources

| Resource | Description |
|----------|-------------|
| [QUICK-START.md](QUICK-START.md) | 30-second setup guide |
| [USAGE.md](USAGE.md) | Detailed examples & advanced usage |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution guidelines |
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [CLAUDE.md](CLAUDE.md) | AI agent configuration for this repo |
| [Agent Index](prompts/english/agents/INDEX.md) | Full agent prompt catalog |
| [Prompt Index](prompts/english/INDEX.md) | All prompts organized by category |
| [Prompt Selector](prompts/english/workflows/prompt-selector-guide.md) | Decision tree for choosing prompts |
| [Workflow Guide](prompts/english/workflows/iterative-development-guide.md) | APEI methodology deep-dive |
| [Troubleshooting Guide](prompts/english/workflows/troubleshooting-guide.md) | Issue diagnosis & resolution flowchart |
| [Claude Code Setup Guide](prompts/english/workflows/claude-code-setup-guide.md) | `.claude/` directory, CLAUDE.md hierarchy, prompt placement |

## Customization

Fork → Modify prompts → Add team standards → Use.

All prompts are MIT-licensed templates. Adapt for your stack, conventions, and tools.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Key areas: new project types, prompt improvements, examples.

## License

MIT License — use, modify, and distribute freely.
