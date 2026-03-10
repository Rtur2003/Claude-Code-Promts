# Prompt Index

All prompts with direct links, organized by category.

## Agent Prompts

Optimized for autonomous AI coding agents (Claude Code, GitHub Copilot, etc.).

| # | Prompt | Purpose | Tokens | File |
|---|--------|---------|--------|------|
| 1 | **Agent System** ⭐ | Core APEI operating system | ~1.5K | [View](agents/claude-agent-system-prompt.md) |
| 2 | **Error Analysis** | Debugging & root cause | ~2K | [View](agents/error-analysis-prompt.md) |
| 3 | **Project Workflow** | Project lifecycle | ~2.5K | [View](agents/project-workflow-prompt.md) |
| 4 | **Quick Reference** | Cheat sheet | ~0.8K | [View](agents/agent-quick-reference.md) |
| 5 | **Code Review** | PR review protocol | ~2K | [View](agents/code-review-prompt.md) |
| 6 | **Security Audit** | Vulnerability detection, cloud & supply chain | ~3.5K | [View](agents/security-audit-prompt.md) |
| 7 | **Refactoring** | Code improvement | ~2.5K | [View](agents/refactoring-prompt.md) |
| 8 | **Testing** | TDD, contract, property & chaos testing | ~4K | [View](agents/testing-strategies-prompt.md) |
| 9 | **Documentation** | Technical writing | ~2.5K | [View](agents/documentation-prompt.md) |
| 10 | **Performance** | Optimization, profiling, CDN & edge | ~3.5K | [View](agents/performance-optimization-prompt.md) |
| 11 | **Git & VCS** | Branching & commits | ~2.5K | [View](agents/git-version-control-prompt.md) |
| 12 | **Integration Guardian** | System integrity | ~3.5K | [View](agents/integration-guardian-prompt.md) |
| 13 | **Claude Code Modes** ⭐ | Mode transitions & planning | ~2.5K | [View](agents/claude-code-modes-prompt.md) |
| 14 | **Claude Code Tokens** | Token optimization strategies | ~2.5K | [View](agents/claude-code-token-optimization-prompt.md) |
| 15 | **Claude Code Workflow** | CLAUDE.md, hooks, permissions | ~3K | [View](agents/claude-code-workflow-prompt.md) |
| 16 | **Technology Stack** ⭐ | Library discovery & modern tools | ~4K | [View](agents/technology-stack-prompt.md) |
| 17 | **Architecture Patterns** | Event sourcing, saga, serverless | ~4.5K | [View](agents/architecture-patterns-prompt.md) |
| 18 | **Full-Stack Development** | End-to-end type-safe, WebSocket, jobs | ~4.5K | [View](agents/fullstack-development-prompt.md) |
| 19 | **Prompt Chaining** | Multi-step workflows | ~3K | [View](agents/prompt-chaining-prompt.md) |
| 20 | **AI & LLM Integration** | RAG, agents, AI safety | ~3.5K | [View](agents/ai-llm-integration-prompt.md) |
| 21 | **Accessibility Audit** | WCAG 2.2, a11y testing | ~3K | [View](agents/accessibility-audit-prompt.md) |
| 22 | **Migration & Upgrade** | Framework & DB migrations | ~2.5K | [View](agents/migration-upgrade-prompt.md) |
| 23 | **Monitoring & Observability** | Logs, metrics, traces | ~3K | [View](agents/monitoring-observability-prompt.md) |
| 24 | **API Design & GraphQL** | Schema-first, DataLoader, contracts | ~4K | [View](agents/api-design-graphql-prompt.md) |
| 25 | **Cloud & Infrastructure** | IaC, multi-region, K8s, cost | ~4K | [View](agents/cloud-infrastructure-prompt.md) |
| 26 | **Data Engineering** | Pipelines, dbt, streaming, quality | ~4K | [View](agents/data-engineering-prompt.md) |
| 27 | **Compliance & Governance** | GDPR, HIPAA, SOC 2, STRIDE | ~3.5K | [View](agents/compliance-governance-prompt.md) |
| 28 | **Debugging & Troubleshooting** | Production debugging, incidents | ~3.5K | [View](agents/debugging-troubleshooting-prompt.md) |

→ [Full Agent Index](agents/INDEX.md)

---

## Foundation Prompt

| Prompt | Purpose | File |
|--------|---------|------|
| **Foundation** ⭐ | Universal best practices, APEI cycle | [View](base/claude-foundation-prompt.md) |

---

## Project-Type Prompts

Use with Foundation prompt for interactive sessions.

| Prompt | Technologies | File |
|--------|-------------|------|
| **Web Development** | React, Vue, Angular, CSS, SEO, A11y | [View](project-types/web-development-prompt.md) |
| **API Development** | REST, GraphQL, Node, Go, idempotency | [View](project-types/api-development-prompt.md) |
| **Data Science & ML** | Python, pandas, scikit-learn, MLOps | [View](project-types/data-science-ml-prompt.md) |
| **Mobile** | iOS, Android, React Native, Flutter | [View](project-types/mobile-development-prompt.md) |
| **DevOps & CI/CD** | Kubernetes, Docker, Terraform | [View](project-types/devops-cicd-prompt.md) |
| **Database & SQL** | PostgreSQL, MySQL, Redis, indexing | [View](project-types/database-sql-prompt.md) |
| **General Software** | Python, JS, Go, Java, C# | [View](project-types/general-software-development-prompt.md) |
| **Game Development** | Unity, Unreal, Godot, ECS, Multiplayer | [View](project-types/game-development-prompt.md) |
| **Embedded & IoT** | C, C++, Rust, FreeRTOS, MQTT, TinyML | [View](project-types/embedded-iot-prompt.md) |
| **Blockchain & Web3** | Solidity, Rust, Foundry, DeFi | [View](project-types/blockchain-web3-prompt.md) |
| **Desktop Apps** | Tauri, Electron, Qt, .NET MAUI | [View](project-types/desktop-development-prompt.md) |

---

## Examples & Guides

| Resource | Description | File |
|----------|-------------|------|
| REST API Example | Building an API step-by-step | [View](examples/rest-api-example.md) |
| Debugging Example | Real-world debugging walkthrough | [View](examples/debugging-example.md) |
| Full-Stack App Example | Next.js + tRPC + Prisma end-to-end | [View](examples/fullstack-app-example.md) |
| Security Audit Example | Vulnerability assessment walkthrough | [View](examples/security-audit-example.md) |
| Refactoring Example | Legacy code improvement walkthrough | [View](examples/refactoring-example.md) |
| Cloud Infrastructure Example | Terraform + K8s deployment walkthrough | [View](examples/cloud-infrastructure-example.md) |
| AI Agent Example | Building an AI-powered code review agent | [View](examples/ai-agent-example.md) |
| Workflow Guide | APEI methodology deep-dive | [View](workflows/iterative-development-guide.md) |
| Prompt Selector | Decision tree for choosing prompts | [View](workflows/prompt-selector-guide.md) |
| Troubleshooting Guide | Issue diagnosis & resolution flowchart | [View](workflows/troubleshooting-guide.md) |

---

## Feature Matrix

| Feature | Foundation | Web | API | Data/ML | Mobile | DevOps | Database | Game | IoT | Full-Stack | Arch | Blockchain | Desktop |
|---------|:---------:|:---:|:---:|:-------:|:------:|:------:|:--------:|:----:|:---:|:----------:|:----:|:----------:|:-------:|
| APEI Cycle | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Commit Standards | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — | ✓ | ✓ |
| Error Analysis | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — | ✓ | ✓ |
| Testing | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — | ✓ | ✓ |
| Component Architecture | — | ✓ | — | — | ✓ | — | — | ✓ | — | ✓ | ✓ | ○ | ✓ |
| Responsive / A11y | — | ✓ | — | — | ✓ | — | — | ○ | — | ○ | — | — | ○ |
| REST / GraphQL Design | — | — | ✓ | — | — | — | — | — | ○ | ✓ | — | — | — |
| Auth Patterns | — | — | ✓ | — | ✓ | — | — | ○ | ✓ | ✓ | — | ✓ | ○ |
| DB Optimization | — | — | ✓ | ○ | — | — | ✓ | — | — | ✓ | — | — | ○ |
| ML Pipeline | — | — | — | ✓ | — | — | — | — | ○ | — | — | — | — |
| CI/CD Pipelines | — | — | — | — | — | ✓ | — | — | ✓ | ○ | — | ○ | ○ |
| Containers / K8s | — | — | — | — | — | ✓ | — | — | — | — | ✓ | — | — |
| Platform-Specific | — | — | — | — | ✓ | — | — | ✓ | ✓ | — | — | ✓ | ✓ |
| Modern Tooling | — | ✓ | ✓ | — | — | — | — | ✓ | — | ✓ | — | ✓ | ✓ |
| System Design | — | — | — | — | — | — | — | — | ✓ | — | ✓ | ✓ | — |
| Type Safety E2E | — | — | ○ | — | — | — | — | — | — | ✓ | — | — | ○ |
| Real-Time / Networking | — | — | ○ | — | — | — | — | ✓ | ✓ | ✓ | — | ✓ | ○ |
| Hardware Integration | — | — | — | — | — | — | — | — | ✓ | — | — | — | ✓ |
| Security / Compliance | — | ○ | ✓ | — | ✓ | ✓ | ○ | — | ✓ | ○ | — | ✓ | ✓ |

✓ = Full  ○ = Partial  — = Not covered
