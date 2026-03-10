# Prompt Selector Guide

Find the right prompt combination in seconds. This guide walks you through selecting prompts based on your mode, task, domain, and token budget.

---

## Decision Tree

```
                        ┌─────────────────────┐
                        │  What are you doing? │
                        └──────────┬──────────┘
                                   │
                 ┌─────────────────┴─────────────────┐
                 ▼                                   ▼
        ┌────────────────┐                  ┌────────────────┐
        │  🤖 AI Agent   │                  │  💬 Interactive │
        │ (Claude Code,  │                  │    Session     │
        │  Copilot, etc) │                  │  (Chat w/ AI)  │
        └───────┬────────┘                  └───────┬────────┘
                │                                   │
                ▼                                   ▼
    ┌───────────────────────┐           ┌───────────────────────┐
    │ Start with:           │           │ Start with:           │
    │ Agent System Prompt   │           │ Foundation Prompt     │
    └───────────┬───────────┘           └───────────┬───────────┘
                │                                   │
                ▼                                   ▼
     ┌─── What's the task? ───┐          ┌── What's the domain? ──┐
     │                        │          │                        │
     ▼          ▼         ▼   ▼          ▼       ▼       ▼       ▼
  ┌──────┐ ┌───────┐ ┌─────┐ ...    ┌──────┐ ┌─────┐ ┌─────┐  ...
  │Build │ │Debug  │ │Review│        │ Web  │ │ API │ │ ML  │
  └──┬───┘ └──┬────┘ └──┬──┘        └──┬───┘ └──┬──┘ └──┬──┘
     │        │         │               │        │       │
     ▼        ▼         ▼               ▼        ▼       ▼
  Project  Error     Code            + Web    + API   + Data
  Workflow Analysis  Review          Dev Prompt  Dev  Science
```

---

## Scenario-Based Selection

> **"I want to..."** → Here's what you need.

### Building & Creating

| Scenario | Agent Mode | Interactive Mode |
|----------|-----------|-----------------|
| Build a new app | Agent System + **Project Workflow** | Foundation + domain prompt |
| Build a full-stack app | Agent System + **Full-Stack Development** | Foundation + **Web** + **API** |
| Choose the right tools | Agent System + **Technology Stack** | Foundation + domain prompt |
| Design system architecture | Agent System + **Architecture Patterns** | Foundation + domain prompt |
| Add AI/LLM features | Agent System + **AI/LLM Integration** | Foundation + **Data Science** |

### Fixing & Improving

| Scenario | Agent Mode | Interactive Mode |
|----------|-----------|-----------------|
| Debug a production issue | Agent System + **Error Analysis** | Foundation + domain prompt |
| Optimize performance | Agent System + **Performance** | Foundation + domain prompt |
| Refactor messy code | Agent System + **Refactoring** | Foundation + domain prompt |
| Upgrade dependencies | Agent System + **Migration & Upgrade** | Foundation + domain prompt |

### Quality & Review

| Scenario | Agent Mode | Interactive Mode |
|----------|-----------|-----------------|
| Review a PR | Agent System + **Code Review** | Foundation + domain prompt |
| Write or improve tests | Agent System + **Testing** | Foundation + domain prompt |
| Audit for security | Agent System + **Security Audit** | Foundation + domain prompt |
| Check accessibility | Agent System + **Accessibility Audit** | Foundation + **Web** |
| Ensure cross-system integrity | Agent System + **Integration Guardian** | Foundation + domain prompt |

### Operations & Documentation

| Scenario | Agent Mode | Interactive Mode |
|----------|-----------|-----------------|
| Set up monitoring | Agent System + **Monitoring & Observability** | Foundation + **DevOps** |
| Write documentation | Agent System + **Documentation** | Foundation + domain prompt |
| Manage Git workflow | Agent System + **Git & VCS** | Foundation + domain prompt |
| Set up CI/CD | Agent System + **Integration Guardian** | Foundation + **DevOps** |

### Claude Code–Specific

| Scenario | Prompt Combination |
|----------|-------------------|
| Use /think and /ultrathink | Agent System + **Mode Transitions** |
| Reduce token usage | Agent System + **Token Optimization** |
| Set up CLAUDE.md & hooks | Agent System + **Workflow & Config** |
| Chain complex multi-step tasks | Agent System + **Prompt Chaining** |

---

## Domain Selection (Interactive Mode)

When using interactive mode, pair `Foundation` with a domain prompt:

```
  Your Project
      │
      ├── Web app (React, Vue, Angular, Svelte) ─────→ + Web Development
      ├── REST / GraphQL API ─────────────────────────→ + API Development
      ├── ML model / data pipeline ───────────────────→ + Data Science & ML
      ├── iOS / Android / Flutter / React Native ─────→ + Mobile
      ├── Kubernetes / Docker / Terraform ────────────→ + DevOps & CI/CD
      ├── Schema design / queries / migrations ───────→ + Database & SQL
      ├── Embedded systems / IoT ─────────────────────→ + Embedded & IoT
      ├── Unity / Unreal / Godot ─────────────────────→ + Game Development
      └── General / multi-language ───────────────────→ + General Software
```

---

## Combination Matrix

Which prompts pair well together, and which are redundant?

### High-Value Combinations (✅ Recommended)

| Primary Prompt | Great With | Why |
|---------------|-----------|-----|
| Project Workflow | Technology Stack | Pick the right tools, then build |
| Error Analysis | Performance | Debug perf issues at root cause |
| Code Review | Security Audit | Catch both quality + security |
| Refactoring | Testing | Refactor safely with test coverage |
| Architecture Patterns | Full-Stack Dev | Design then implement |
| Migration & Upgrade | Testing | Validate upgrades don't break things |
| Documentation | Code Review | Ensure docs match the code |
| Monitoring | Performance | Monitor what you've optimized |

### Redundant Combinations (⚠️ Avoid)

| Combo | Why It's Redundant |
|-------|-------------------|
| Project Workflow + Full-Stack Dev | Both cover project setup — pick one |
| Quick Reference + Agent System | Quick Reference is a subset of Agent System |
| Architecture + Technology Stack | Significant overlap in tech decisions |
| Mode Transitions + Token Optimization | Use one at a time; both are Claude Code meta-prompts |

---

## Token Budget Calculator

Choose your setup based on available context window space.

```
  ┌────────────────────────────────────────────────────────────────┐
  │                    TOKEN BUDGET GUIDE                          │
  ├───────────┬────────────────────────────────────────────────────┤
  │           │                                                    │
  │  < 2K     │  Quick Reference only                              │
  │  tokens   │  ● Best for: simple one-off tasks                  │
  │           │  ● Tokens: ~800                                    │
  │           │                                                    │
  ├───────────┼────────────────────────────────────────────────────┤
  │           │                                                    │
  │  2K – 8K  │  Agent System OR Foundation (one core prompt)      │
  │  tokens   │  ● Best for: standard development tasks            │
  │           │  ● Room for: 1 specialty prompt if needed          │
  │           │  ● Example: Agent System + Error Analysis (~3.5K)  │
  │           │                                                    │
  ├───────────┼────────────────────────────────────────────────────┤
  │           │                                                    │
  │  8K – 16K │  Core prompt + 2–3 specialty prompts               │
  │  tokens   │  ● Best for: complex or multi-concern tasks        │
  │           │  ● Example: Agent System + Code Review             │
  │           │    + Security Audit + Testing (~9.5K)               │
  │           │                                                    │
  ├───────────┼────────────────────────────────────────────────────┤
  │           │                                                    │
  │  16K+     │  Core + multiple specialties + project-type        │
  │  tokens   │  ● Best for: full project bootstraps               │
  │           │  ● Example: Agent System + Project Workflow         │
  │           │    + Full-Stack Dev + Testing + Security (~14K)     │
  │           │                                                    │
  └───────────┴────────────────────────────────────────────────────┘
```

### Quick Token Reference

| Prompt | ~Tokens |
|--------|---------|
| Quick Reference | 0.8K |
| Agent System | 1.5K |
| Error Analysis | 2K |
| Code Review | 2K |
| Project Workflow | 2.5K |
| Security Audit | 2.5K |
| Refactoring | 2.5K |
| Documentation | 2.5K |
| Git & VCS | 2.5K |
| Mode Transitions | 2.5K |
| Token Optimization | 2.5K |
| Workflow & Config | 3K |
| Testing | 3K |
| Performance | 3K |
| Prompt Chaining | 3K |
| Architecture Patterns | 3.5K |
| Full-Stack Dev | 3.5K |
| Integration Guardian | 3.5K |
| Technology Stack | 4K |

---

## Anti-Patterns

### ❌ Don't: Load Every Prompt at Once

```
# BAD — wastes tokens, causes conflicting instructions
Agent System + Error Analysis + Project Workflow + Code Review
+ Security Audit + Refactoring + Testing + Documentation
+ Performance + Git + Integration Guardian  ← ~28K tokens!
```

**Why:** Prompts may give conflicting priorities. The AI spends tokens parsing instructions instead of solving your problem.

**Do instead:** Pick 1 core prompt + 1–2 relevant specialties.

### ❌ Don't: Use Project-Type Prompts in Agent Mode

```
# BAD — project-type prompts are designed for interactive sessions
Agent System + Web Development Prompt
```

**Why:** Project-type prompts (Web, API, Mobile, etc.) assume a conversational back-and-forth flow. Agent prompts already include domain-aware behavior.

**Do instead:** Use agent specialty prompts (Performance, Security, etc.) which are built for autonomous operation.

### ❌ Don't: Stack Multiple Meta-Prompts

```
# BAD — meta-prompts about how to use Claude Code conflict
Mode Transitions + Token Optimization + Workflow & Config
```

**Why:** These are all "how to operate" prompts. Using more than one creates contradictory operational directives.

**Do instead:** Pick the one most relevant to your current need.

### ❌ Don't: Use Agent System + Quick Reference Together

```
# BAD — Quick Reference is a compressed subset
Agent System + Quick Reference
```

**Why:** Quick Reference is a minimal version of Agent System. Using both wastes tokens on duplicate content.

**Do instead:** Pick one — Agent System for full tasks, Quick Reference when tokens are tight.

### ❌ Don't: Skip the Core Prompt

```
# BAD — specialty prompts assume core context
Error Analysis (alone, no Agent System)
```

**Why:** Specialty prompts build on the APEI methodology defined in the core prompts. Without the core, the AI lacks the structured reasoning framework.

**Do instead:** Always start with Agent System (agent mode) or Foundation (interactive mode).

---

## Quick Lookup Cheat Sheet

```
  ┌──────────────────────────────────────────────────────────┐
  │                  PROMPT SELECTOR                         │
  │                                                          │
  │  Agent?  → Agent System + task prompt                    │
  │  Chat?   → Foundation + domain prompt                    │
  │                                                          │
  │  Building?    → + Project Workflow / Full-Stack          │
  │  Debugging?   → + Error Analysis                        │
  │  Reviewing?   → + Code Review                           │
  │  Optimizing?  → + Performance                           │
  │  Securing?    → + Security Audit                        │
  │  Testing?     → + Testing                               │
  │  Refactoring? → + Refactoring                           │
  │  Documenting? → + Documentation                         │
  │  Migrating?   → + Migration & Upgrade                   │
  │  Monitoring?  → + Monitoring & Observability            │
  │  AI features? → + AI/LLM Integration                    │
  │  Accessibility?→ + Accessibility Audit                  │
  │                                                          │
  │  Low tokens?  → Quick Reference only                    │
  │  Claude Code? → + Mode Transitions or Token Optimization│
  └──────────────────────────────────────────────────────────┘
```

---

## See Also

- [README.md](../../../README.md) — Full prompt catalog
- [QUICK-START.md](../../../QUICK-START.md) — 30-second setup
- [USAGE.md](../../../USAGE.md) — Detailed examples
- [Iterative Development Guide](iterative-development-guide.md) — APEI deep-dive
- [Agent Index](../agents/INDEX.md) — All agent prompts
- [Prompt Index](../INDEX.md) — All prompts by category
