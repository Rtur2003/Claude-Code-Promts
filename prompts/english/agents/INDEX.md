# Agent Prompts Index

> **Optimized for AI Coding Agents** | **Claude Code, GitHub Copilot, etc.**

## Overview

These prompts are specifically designed for autonomous AI coding agents. They are:

- ✅ **Token-Optimized**: Minimal tokens for maximum effectiveness
- ✅ **Agent-Ready**: Structured for autonomous operation
- ✅ **Action-Oriented**: Clear commands and workflows
- ✅ **Universal**: Work with any codebase or language

---

## Available Prompts

### 1. Claude Agent System Prompt ⭐ (Start Here)
**File**: [claude-agent-system-prompt.md](claude-agent-system-prompt.md)

**Purpose**: Core operating system for AI coding agents. Contains the APEI loop (Analyze → Plan → Execute → Iterate) and all foundational behaviors.

**Use When**:
- Starting any coding task
- Need a complete agent system prompt
- Want systematic, iterative development

**Key Features**:
- APEI development cycle
- Commit standards
- Code quality checklist
- Communication templates
- Token optimization tips

---

### 2. Error Analysis Prompt 🔍
**File**: [error-analysis-prompt.md](error-analysis-prompt.md)

**Purpose**: Systematic error detection, root cause analysis, and resolution.

**Use When**:
- Debugging failing builds
- Fixing test failures
- Resolving runtime errors
- Investigating security issues

**Key Features**:
- Automatic error scanning commands
- Error classification (P0-P3)
- Root cause analysis (5 Whys)
- Fix implementation process
- Prevention strategies

---

### 3. Project Workflow Prompt 📊
**File**: [project-workflow-prompt.md](project-workflow-prompt.md)

**Purpose**: End-to-end project management from assessment to maintenance.

**Use When**:
- Starting a new project
- Taking over existing codebase
- Planning feature development
- Improving project health

**Key Features**:
- Project assessment framework
- Goal definition templates
- Feature breakdown structure
- Testing strategy
- Maintenance checklists

---

### 4. Quick Reference Card 📋
**File**: [agent-quick-reference.md](agent-quick-reference.md)

**Purpose**: Ultra-concise reference for common patterns and commands.

**Use When**:
- Need quick reminder of formats
- Want copy-paste templates
- Looking up common commands
- Memory-constrained context

**Key Features**:
- All templates in one page
- Common commands cheat sheet
- Checklist quick reference
- Debug workflow summary

---

### 5. Code Review Prompt 🔍
**File**: [code-review-prompt.md](code-review-prompt.md)

**Purpose**: Systematic code review with quality assurance and best practices.

**Use When**:
- Reviewing pull requests
- Self-reviewing code before commit
- Establishing code review standards
- Training on review best practices

**Key Features**:
- Four-phase review protocol
- Common code patterns to watch for
- Feedback templates (Blocker, Warning, Suggestion)
- File-type specific checklists

---

### 6. Security Audit Prompt 🔐
**File**: [security-audit-prompt.md](security-audit-prompt.md)

**Purpose**: Comprehensive security vulnerability detection and remediation.

**Use When**:
- Auditing application security
- Reviewing code for vulnerabilities
- Implementing security best practices
- Preparing for security assessments

**Key Features**:
- OWASP Top 10 checklist
- Vulnerability severity matrix
- Automated scanning commands
- Remediation code examples

---

### 7. Refactoring Prompt ♻️
**File**: [refactoring-prompt.md](refactoring-prompt.md)

**Purpose**: Systematic code improvement and technical debt reduction.

**Use When**:
- Improving code quality
- Reducing technical debt
- Preparing for new features
- Code cleanup sessions

**Key Features**:
- Code smell detection
- SAFE refactoring protocol
- Common refactoring patterns
- Before/after comparisons

---

### 8. Testing Strategies Prompt 🧪
**File**: [testing-strategies-prompt.md](testing-strategies-prompt.md)

**Purpose**: Comprehensive testing design and implementation guidance.

**Use When**:
- Designing test strategies
- Implementing TDD
- Improving test coverage
- Writing different test types

**Key Features**:
- TEST protocol (Target, Engineer, Specify, Track)
- Unit, integration, E2E examples
- Performance testing with k6
- Coverage tracking templates

---

## How to Use

### Option 1: Full Agent Setup
Use the **Claude Agent System Prompt** as your base. It contains everything needed for autonomous operation.

```
[Provide claude-agent-system-prompt.md content to the AI]

Now, please analyze this codebase and propose improvements...
```

### Option 2: Task-Specific
Add specialized prompts for specific tasks:

**For debugging**:
```
[Base prompt] + [Error Analysis Prompt]
```

**For project development**:
```
[Base prompt] + [Project Workflow Prompt]
```

### Option 3: Quick Reference Only
For simple tasks or when context is limited:
```
[Quick Reference Card only]
```

---

## Comparison: Agent vs Traditional Prompts

| Feature | Traditional Prompts | Agent Prompts |
|---------|-------------------|---------------|
| Length | Verbose | Token-optimized |
| Structure | Descriptive | Action-oriented |
| Output | Suggestions | Autonomous execution |
| Workflow | Manual guidance | Self-directing loops |
| Error Handling | Reactive | Proactive + preventive |

---

## Combining with Project-Type Prompts

Agent prompts work well combined with project-type prompts:

### Web Development
```
[Claude Agent System] + [Web Development Prompt]
```

### API Development
```
[Claude Agent System] + [API Development Prompt]
```

### Data Science
```
[Claude Agent System] + [Data Science Prompt]
```

---

## Token Optimization Guide

### Minimal Context (Under 2K tokens)
Use: **Quick Reference Card** only

### Standard Context (2K-8K tokens)
Use: **Claude Agent System Prompt**

### Extended Context (8K+ tokens)
Use: **Full combination** with project-type prompts

---

## Prompt Effectiveness

All agent prompts are designed for:

1. **Autonomous Operation**: Agents can work with minimal human intervention
2. **Self-Correction**: Built-in iteration loops catch and fix issues
3. **Quality Assurance**: Checklists and validation at every step
4. **Clear Communication**: Structured reporting formats
5. **Efficient Token Usage**: Maximum value per token

---

## Best Practices

### DO ✅
- Start with the Agent System Prompt
- Let the agent complete the APEI cycle
- Trust the iterative process
- Use Quick Reference for simple tasks

### DON'T ❌
- Interrupt mid-cycle unnecessarily
- Skip the analysis phase
- Ignore test failures
- Rush to "done" without validation

---

## Feedback & Improvement

These prompts are continuously improved based on real-world usage. Key metrics:

- Task completion rate
- Error rate reduction
- Token efficiency
- User satisfaction

Found an improvement? The prompts themselves follow the APEI cycle for enhancement.
