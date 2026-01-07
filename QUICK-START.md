# Quick Reference Guide

**Fast access to Claude system prompts**

## 🚀 Quick Start (30 seconds)

1. **Pick a prompt**: See options below
2. **Copy content**: Open the markdown file
3. **Give to Claude**: Paste at start of session
4. **Start coding**: Follow the methodology

## 🤖 Agent Prompts (For AI Coding Agents)

**Best for**: Claude Code, GitHub Copilot, autonomous coding tasks

| Prompt | Use Case | File |
|--------|----------|------|
| **Agent System** ⭐ | All autonomous tasks | [claude-agent-system-prompt.md](prompts/english/agents/claude-agent-system-prompt.md) |
| **Error Analysis** | Debugging & fixes | [error-analysis-prompt.md](prompts/english/agents/error-analysis-prompt.md) |
| **Project Workflow** | Full project lifecycle | [project-workflow-prompt.md](prompts/english/agents/project-workflow-prompt.md) |
| **Quick Reference** | Cheat sheet (minimal tokens) | [agent-quick-reference.md](prompts/english/agents/agent-quick-reference.md) |
| **Code Review** | Systematic PR reviews | [code-review-prompt.md](prompts/english/agents/code-review-prompt.md) |
| **Security Audit** | Vulnerability detection | [security-audit-prompt.md](prompts/english/agents/security-audit-prompt.md) |
| **Refactoring** | Code improvement | [refactoring-prompt.md](prompts/english/agents/refactoring-prompt.md) |
| **Testing Strategies** | Test design & TDD | [testing-strategies-prompt.md](prompts/english/agents/testing-strategies-prompt.md) |
| **Documentation** | Technical writing | [documentation-prompt.md](prompts/english/agents/documentation-prompt.md) |
| **Performance** | Optimization | [performance-optimization-prompt.md](prompts/english/agents/performance-optimization-prompt.md) |

👉 **[Full Agent Prompts Index](prompts/english/agents/INDEX.md)**

## 🌍 Türkçe Prompt'lar (Turkish)

- **[Türkçe Agent Sistem](prompts/turkish/agents/claude-agent-system-prompt-tr.md)** - AI ajanları için temel sistem
- **[Türkçe Temel Prompt](prompts/turkish/base/claude-foundation-prompt-tr.md)** - Evrensel en iyi uygulamalar

👉 **[Türkçe İndeks](prompts/turkish/INDEX.md)**

## 📋 Traditional Prompts (For Interactive Sessions)

### For Everyone
- **[Foundation Prompt](prompts/english/base/claude-foundation-prompt.md)** - Start here, universal best practices

### By Project Type
- **[Web Development](prompts/english/project-types/web-development-prompt.md)** - React, Vue, HTML/CSS
- **[API Development](prompts/english/project-types/api-development-prompt.md)** - REST, GraphQL, Backend
- **[Data Science & ML](prompts/english/project-types/data-science-ml-prompt.md)** - Python, ML, Data Analysis
- **[Mobile Development](prompts/english/project-types/mobile-development-prompt.md)** - iOS, Android, React Native, Flutter
- **[DevOps & CI/CD](prompts/english/project-types/devops-cicd-prompt.md)** - Kubernetes, Docker, Pipelines
- **[General Software](prompts/english/project-types/general-software-development-prompt.md)** - Multi-language

### Examples
- **[REST API Example](prompts/english/examples/rest-api-example.md)** - Building a REST API step-by-step

### Learn the Process
- **[Workflow Guide](prompts/english/workflows/iterative-development-guide.md)** - How to iterate effectively

## 🎯 Common Use Cases

| What You're Building | Use These Prompts |
|---------------------|-------------------|
| AI Agent Task | Agent System (alone) |
| Debug/Fix Bugs | Agent System + Error Analysis |
| New Project | Agent System + Project Workflow |
| Code Review | Agent System + Code Review |
| Security Audit | Agent System + Security Audit |
| Refactoring | Agent System + Refactoring |
| Test Suite | Agent System + Testing Strategies |
| React App | Foundation + Web Development |
| REST API | Foundation + API Development |
| ML Model | Foundation + Data Science & ML |
| Mobile App | Foundation + Mobile Development |
| DevOps/Infra | Foundation + DevOps & CI/CD |
| Full-Stack App | Foundation + Web + API |
| Python Script | Foundation + General Software |
| Any Project | Foundation (at minimum) |

## 💡 The Core Method

All prompts follow this cycle:

```
1. ANALYZE - Understand the problem
   ↓
2. PLAN - Design minimal solution
   ↓
3. EXECUTE - Implement step-by-step with tests
   ↓
4. EVALUATE - Check if optimal
   ↓
If not optimal → Back to step 1
If optimal → Done ✓
```

## 📚 Full Documentation

- **[README.md](README.md)** - Complete overview
- **[USAGE.md](USAGE.md)** - Detailed examples
- **[INDEX.md](prompts/english/INDEX.md)** - All prompts with descriptions

## 🔑 Key Features

Every prompt includes:
- ✅ Quality-focused development practices
- ✅ Commit message standards
- ✅ Error analysis methodology
- ✅ Testing strategies
- ✅ Iterative improvement cycle
- ✅ Security considerations
- ✅ Performance guidelines

## 📝 Example Session Start

### For AI Agents (Claude Code, Copilot)

```
[Paste Agent System Prompt content]

Analyze this codebase and:
1. Identify any bugs or issues
2. Propose improvements
3. Fix the most critical issues
```

### For Interactive Sessions

```
Hi Claude! I'm building a REST API for a blog platform.

Please use this system prompt:
[Copy/paste content of Foundation + API Development prompts]

Requirements:
- User authentication (JWT)
- CRUD for blog posts
- Comment system

Let's start by analyzing the requirements and creating a plan.
```

## ⚡ Pro Tips

### For AI Agents
1. **Use Agent System Prompt**: It's designed for autonomous operation
2. **Let it iterate**: Trust the APEI cycle (Analyze → Plan → Execute → Iterate)
3. **Be specific**: Clear goals lead to better results
4. **Review checkpoints**: Check progress at each iteration

### For Interactive Sessions
1. **Start Simple**: Use just Foundation for most projects
2. **Add Specialization**: Layer on domain prompts as needed
3. **Trust the Process**: Let Claude follow the Analyze-Plan-Execute cycle
4. **Test Often**: Validate after each small change
5. **Know When to Stop**: Optimal is better than perfect

## 🎓 Learning Path

### For AI Agents
1. Read **Agent System Prompt** (5 min)
2. Try a simple task with the prompt
3. Review **Quick Reference Card** for shortcuts
4. Add **Error Analysis** prompt for debugging tasks

### For Interactive Sessions
1. Read **Foundation Prompt** (10 min)
2. Skim your **project-specific prompt** (5 min)
3. Review **Workflow Guide** (15 min)
4. Start building with Claude!

## 🤝 Getting Help

- Questions? Check [USAGE.md](USAGE.md)
- Need examples? See [Workflow Guide](prompts/english/workflows/iterative-development-guide.md)
- Want to contribute? See [README.md](README.md)

---

**Remember**: These prompts help Claude help you build better software through systematic iteration and quality focus.

**Time to start?** Pick your prompt(s) above and begin! 🚀
