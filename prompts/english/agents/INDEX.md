# Agent Prompts Index

> Outcome-first catalog for autonomous AI coding agents.

## Core Rule

Start with [Agent System](claude-agent-system-prompt.md). Add one specialist prompt only if required.

## Active Catalog (Keep)

| Prompt | Use when | Do not use when | File |
|--------|----------|-----------------|------|
| Agent System ⭐ | Any autonomous task | You only need minimal guidance | [View](claude-agent-system-prompt.md) |
| Quick Reference | Token budget is extremely tight | You need specialist depth | [View](agent-quick-reference.md) |
| Code Review | Reviewing a PR/change set | Writing a feature from scratch | [View](code-review-prompt.md) |
| Security Audit | Security risk is material | No threat model is in scope | [View](security-audit-prompt.md) |
| Refactoring | Reducing complexity safely | Active production incident | [View](refactoring-prompt.md) |
| Testing | Building test strategy and coverage | You only need docs | [View](testing-strategies-prompt.md) |
| Documentation | Producing high-quality docs | Root-cause debugging task | [View](documentation-prompt.md) |
| Performance | Throughput/latency/cost bottlenecks | Core issue is correctness | [View](performance-optimization-prompt.md) |
| Git & VCS | Branching/commit/release hygiene | App architecture decision | [View](git-version-control-prompt.md) |
| Accessibility Audit | Accessibility and WCAG compliance | Backend-only systems task | [View](accessibility-audit-prompt.md) |
| Migration & Upgrade | Framework/runtime/DB migration | Greenfield build | [View](migration-upgrade-prompt.md) |
| Monitoring & Observability | Logs/metrics/traces/alerts | Pure content update | [View](monitoring-observability-prompt.md) |
| Debugging & Troubleshooting | Incident/root-cause diagnostics | Net-new architecture design | [View](debugging-troubleshooting-prompt.md) |
| Claude Code Modes ⭐ | Managing Claude Code thinking modes | Non-Claude context only | [View](claude-code-modes-prompt.md) |
| Claude Code Workflow | CLAUDE.md/hooks/permissions/MCP | No Claude Code setup task | [View](claude-code-workflow-prompt.md) |
| Technology Stack ⭐ | Tool/library selection | Stack already fixed | [View](technology-stack-prompt.md) |
| Architecture Patterns | Architecture and trade-off design | Small local fix | [View](architecture-patterns-prompt.md) |
| Full-Stack Development | End-to-end web app delivery | Narrow scoped layer-only task | [View](fullstack-development-prompt.md) |
| AI & LLM Integration | RAG/vector/agent integration | No AI component exists | [View](ai-llm-integration-prompt.md) |
| API Design & GraphQL | API contracts/schema decisions | UI-only work | [View](api-design-graphql-prompt.md) |
| Cloud & Infrastructure | IaC/K8s/multi-region operations | Pure local utility task | [View](cloud-infrastructure-prompt.md) |
| Data Engineering | Pipelines/streaming/data quality | Standard app CRUD only | [View](data-engineering-prompt.md) |
| Compliance & Governance | Regulated scope and controls | Non-regulated prototype | [View](compliance-governance-prompt.md) |
| Multi-Agent Orchestration | Coordinating parallel agents | Single-agent linear work | [View](multi-agent-orchestration-prompt.md) |
| Monorepo & Complex Projects | Multi-package coordination | Small standalone repo | [View](monorepo-complex-projects-prompt.md) |
| Error Handling & Resilience | Fault tolerance and reliability | Static content updates | [View](error-handling-resilience-prompt.md) |
| Developer Experience & Tooling | Lint/hooks/dev workflow standards | Core feature implementation | [View](developer-experience-tooling-prompt.md) |
| Database Design & Optimization | Schema/index/query optimization | No data layer scope | [View](database-optimization-prompt.md) |
| UI/UX & Design Systems | Component systems/theming/a11y UI | Backend-only task | [View](ui-design-systems-prompt.md) |

## Archived (Merge/Archive)

| Prompt | Status | Merged Into | File |
|--------|--------|-------------|------|
| Error Analysis | Archive | Debugging & Troubleshooting + Agent System | [View](archive/error-analysis-prompt.md) |
| Project Workflow | Archive | Agent System + Technology Stack + Full-Stack Development | [View](archive/project-workflow-prompt.md) |
| Integration Guardian | Archive | Code Review + Testing + Monitoring & Observability | [View](archive/integration-guardian-prompt.md) |
| Claude Code Token Optimization | Archive | Claude Code Modes + Claude Code Workflow | [View](archive/claude-code-token-optimization-prompt.md) |
| Prompt Chaining | Archive | Agent System + Multi-Agent Orchestration | [View](archive/prompt-chaining-prompt.md) |

See full rationale in [Archive Index](archive/INDEX.md).
