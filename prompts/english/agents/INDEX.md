# Agent Prompts Index

> Optimized for autonomous AI coding agents — Claude Code, GitHub Copilot, etc.

## Catalog

| # | Prompt | Purpose | Tokens | File |
|---|--------|---------|--------|------|
| 1 | **Agent System** ⭐ | Core APEI operating system | ~1.5K | [View](claude-agent-system-prompt.md) |
| 2 | **Error Analysis** | Debugging & root cause analysis | ~2K | [View](error-analysis-prompt.md) |
| 3 | **Project Workflow** | End-to-end project lifecycle | ~2.5K | [View](project-workflow-prompt.md) |
| 4 | **Quick Reference** | Cheat sheet (minimal tokens) | ~0.8K | [View](agent-quick-reference.md) |
| 5 | **Code Review** | Systematic PR review | ~2K | [View](code-review-prompt.md) |
| 6 | **Security Audit** | Vulnerability detection (OWASP) | ~2.5K | [View](security-audit-prompt.md) |
| 7 | **Refactoring** | Code smell detection & SAFE protocol | ~2.5K | [View](refactoring-prompt.md) |
| 8 | **Testing** | TEST protocol, TDD, coverage | ~3K | [View](testing-strategies-prompt.md) |
| 9 | **Documentation** | CLEAR protocol, API docs | ~2.5K | [View](documentation-prompt.md) |
| 10 | **Performance** | MEASURE protocol, profiling | ~3K | [View](performance-optimization-prompt.md) |
| 11 | **Git & VCS** | BRANCH protocol, commits | ~2.5K | [View](git-version-control-prompt.md) |
| 12 | **Integration Guardian** | i18n, tokens, contracts, a11y | ~0.5K | [View](integration-guardian-prompt.md) |
| 13 | **Claude Code Modes** ⭐ | Mode transitions, /think, /ultrathink | ~2.5K | [View](claude-code-modes-prompt.md) |
| 14 | **Claude Code Tokens** | Token optimization, SAVE protocol | ~2.5K | [View](claude-code-token-optimization-prompt.md) |
| 15 | **Claude Code Workflow** | CLAUDE.md, hooks, permissions, MCP | ~3K | [View](claude-code-workflow-prompt.md) |
| 16 | **Technology Stack** ⭐ | Library discovery, modern tools, hidden gems | ~4K | [View](technology-stack-prompt.md) |
| 17 | **Architecture Patterns** | System design, microservices, DDD, CQRS | ~3.5K | [View](architecture-patterns-prompt.md) |
| 18 | **Full-Stack Development** | Next.js/Nuxt/SvelteKit, end-to-end type safety | ~3.5K | [View](fullstack-development-prompt.md) |
| 19 | **Prompt Chaining** | Multi-step workflows, context management | ~3K | [View](prompt-chaining-prompt.md) |

---

## Claude Code-Specific

These prompts are designed specifically for Claude Code's native features:

| Task | Combine With |
|------|-------------|
| Mode planning | Claude Code Modes |
| Token efficiency | Claude Code Tokens |
| Project setup | Claude Code Workflow |
| Full Claude Code setup | Modes + Tokens + Workflow |

---

## Usage

### Option 1: Full Agent Setup
Use **Agent System Prompt** as base. It contains everything for autonomous operation.

### Option 2: Task-Specific
Combine Agent System + specialist prompt:

| Task | Combine With |
|------|-------------|
| Debugging | Error Analysis |
| New project | Project Workflow |
| PR review | Code Review |
| Security check | Security Audit |
| Tech debt | Refactoring |
| Test coverage | Testing |
| Writing docs | Documentation |
| Slow code | Performance |
| Git workflow | Git & VCS |
| System integrity | Integration Guardian |
| Tool/library selection | Technology Stack |
| System architecture | Architecture Patterns |
| Full-stack app | Full-Stack Development |
| Complex multi-step task | Prompt Chaining |

### Option 3: Minimal Context
Use **Quick Reference** alone when token budget is tight (< 2K).

---

## Token Budget Guide

| Budget | Recommended |
|--------|-------------|
| < 2K tokens | Quick Reference only |
| 2K–8K tokens | Agent System Prompt |
| 8K+ tokens | Agent System + specialist + project-type |

---

## Agent vs Traditional Prompts

| Feature | Traditional | Agent |
|---------|:-----------:|:-----:|
| Token usage | Verbose | Optimized |
| Structure | Descriptive | Action-oriented |
| Execution | Manual guidance | Autonomous |
| Error handling | Reactive | Proactive |
| Workflow | Linear | Self-directing loops |
