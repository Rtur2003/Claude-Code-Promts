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
| 6 | **Security Audit** | Vulnerability detection | ~2.5K | [View](agents/security-audit-prompt.md) |
| 7 | **Refactoring** | Code improvement | ~2.5K | [View](agents/refactoring-prompt.md) |
| 8 | **Testing** | Test design & TDD | ~3K | [View](agents/testing-strategies-prompt.md) |
| 9 | **Documentation** | Technical writing | ~2.5K | [View](agents/documentation-prompt.md) |
| 10 | **Performance** | Optimization & profiling | ~3K | [View](agents/performance-optimization-prompt.md) |
| 11 | **Git & VCS** | Branching & commits | ~2.5K | [View](agents/git-version-control-prompt.md) |
| 12 | **Integration Guardian** | System integrity | ~0.5K | [View](agents/integration-guardian-prompt.md) |
| 13 | **Claude Code Modes** ⭐ | Mode transitions & planning | ~2.5K | [View](agents/claude-code-modes-prompt.md) |
| 14 | **Claude Code Tokens** | Token optimization strategies | ~2.5K | [View](agents/claude-code-token-optimization-prompt.md) |
| 15 | **Claude Code Workflow** | CLAUDE.md, hooks, permissions | ~3K | [View](agents/claude-code-workflow-prompt.md) |
| 16 | **Technology Stack** ⭐ | Library discovery & modern tools | ~4K | [View](agents/technology-stack-prompt.md) |
| 17 | **Architecture Patterns** | System design, DDD, CQRS | ~3.5K | [View](agents/architecture-patterns-prompt.md) |
| 18 | **Full-Stack Development** | End-to-end type-safe full-stack | ~3.5K | [View](agents/fullstack-development-prompt.md) |
| 19 | **Prompt Chaining** | Multi-step workflows | ~3K | [View](agents/prompt-chaining-prompt.md) |

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
| **Web Development** | React, Vue, Angular, CSS, A11y | [View](project-types/web-development-prompt.md) |
| **API Development** | REST, GraphQL, Node, Go, Java | [View](project-types/api-development-prompt.md) |
| **Data Science & ML** | Python, pandas, scikit-learn, PyTorch | [View](project-types/data-science-ml-prompt.md) |
| **Mobile** | iOS, Android, React Native, Flutter | [View](project-types/mobile-development-prompt.md) |
| **DevOps & CI/CD** | Kubernetes, Docker, Terraform | [View](project-types/devops-cicd-prompt.md) |
| **Database & SQL** | PostgreSQL, MySQL, Redis, indexing | [View](project-types/database-sql-prompt.md) |
| **General Software** | Python, JS, Go, Java, C# | [View](project-types/general-software-development-prompt.md) |

---

## Examples & Guides

| Resource | Description | File |
|----------|-------------|------|
| REST API Example | Building an API step-by-step | [View](examples/rest-api-example.md) |
| Debugging Example | Real-world debugging walkthrough | [View](examples/debugging-example.md) |
| Workflow Guide | APEI methodology deep-dive | [View](workflows/iterative-development-guide.md) |

---

## Feature Matrix

| Feature | Foundation | Web | API | Data/ML | Mobile | DevOps | Database | Full-Stack | Arch |
|---------|:---------:|:---:|:---:|:-------:|:------:|:------:|:--------:|:----------:|:----:|
| APEI Cycle | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Commit Standards | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Error Analysis | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Testing | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Component Architecture | — | ✓ | — | — | ✓ | — | — | ✓ | ✓ |
| Responsive / A11y | — | ✓ | — | — | ✓ | — | — | ○ | — |
| REST / GraphQL Design | — | — | ✓ | — | — | — | — | ✓ | — |
| Auth Patterns | — | — | ✓ | — | ✓ | — | — | ✓ | — |
| DB Optimization | — | — | ✓ | ○ | — | — | ✓ | ✓ | — |
| ML Pipeline | — | — | — | ✓ | — | — | — | — | — |
| CI/CD Pipelines | — | — | — | — | — | ✓ | — | ○ | — |
| Containers / K8s | — | — | — | — | — | ✓ | — | — | ✓ |
| Platform-Specific | — | — | — | — | ✓ | — | — | — | — |
| Modern Tooling | — | ✓ | ✓ | — | — | — | — | ✓ | — |
| System Design | — | — | — | — | — | — | — | — | ✓ |
| Type Safety E2E | — | — | ○ | — | — | — | — | ✓ | — |

✓ = Full  ○ = Partial  — = Not covered

---

## Language Support

| Language | Status | Link |
|----------|--------|------|
| English | ✅ Complete | This index |
| Türkçe | 🔄 In Progress | [Turkish Index](../turkish/INDEX.md) |
