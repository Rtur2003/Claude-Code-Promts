# Claude Code Prompts

A comprehensive collection of system prompts for Claude AI to achieve optimal software development results through iterative, quality-focused workflows.

## 🚀 NEW: Agent-Optimized Prompts

**Now with prompts specifically designed for AI coding agents!**

These new prompts are optimized for autonomous operation with Claude Code, GitHub Copilot, and similar AI coding assistants:

| Prompt | Purpose | Tokens |
|--------|---------|--------|
| [**Agent System**](prompts/english/agents/claude-agent-system-prompt.md) | Core operating system for AI agents | ~1.5K |
| [**Error Analysis**](prompts/english/agents/error-analysis-prompt.md) | Systematic debugging & fixes | ~2K |
| [**Project Workflow**](prompts/english/agents/project-workflow-prompt.md) | Full project lifecycle management | ~2.5K |
| [**Quick Reference**](prompts/english/agents/agent-quick-reference.md) | Token-optimized cheat sheet | ~0.8K |
| [**Code Review**](prompts/english/agents/code-review-prompt.md) | Systematic code review | ~2K |
| [**Security Audit**](prompts/english/agents/security-audit-prompt.md) | Vulnerability detection & remediation | ~2.5K |
| [**Refactoring**](prompts/english/agents/refactoring-prompt.md) | Code improvement patterns | ~2.5K |
| [**Testing Strategies**](prompts/english/agents/testing-strategies-prompt.md) | Comprehensive testing guidance | ~3K |
| [**Documentation**](prompts/english/agents/documentation-prompt.md) | Technical writing & API docs | ~2.5K |
| [**Performance**](prompts/english/agents/performance-optimization-prompt.md) | Optimization & profiling | ~3K |
| [**Git & Version Control**](prompts/english/agents/git-version-control-prompt.md) | Branching, commits, collaboration | ~2.5K |

### Why Agent Prompts?

- ✅ **Token-Efficient**: Maximum effectiveness with minimal tokens
- ✅ **Autonomous**: Agents work with minimal human intervention
- ✅ **Self-Correcting**: Built-in iteration loops catch and fix issues
- ✅ **Universal**: Work with any codebase, language, or framework

👉 **[View Agent Prompts Index](prompts/english/agents/INDEX.md)**

---

## 🌍 Language Support

| Language | Status | Link |
|----------|--------|------|
| English | ✅ Complete (13 agent + 7 project prompts) | [prompts/english/](prompts/english/INDEX.md) |
| Türkçe | 🔄 In Progress (4 prompts) | [prompts/turkish/](prompts/turkish/INDEX.md) |

---

## Overview

This repository provides **production-ready system prompts** that enable Claude to follow industry best practices, maintain high code quality, and work through an iterative development cycle until reaching optimal solutions.

### Core Philosophy: Analyze → Plan → Execute → Iterate (APEI)

All prompts follow a systematic approach:
1. **Analyze**: Understand the problem completely
2. **Plan**: Design minimal, focused solutions
3. **Execute**: Implement step-by-step with continuous validation
4. **Iterate**: Refine until optimal

## Features

- 🤖 **Agent-Ready**: Optimized prompts for AI coding agents
- 🎯 **Quality-Focused**: Emphasizes code quality, testing, and maintainability
- 🔄 **Iterative Development**: Continuous improvement cycle until optimal
- 📚 **Comprehensive Coverage**: Commits, error analysis, testing, deployment
- 🏗️ **Project-Specific**: Tailored prompts for different development types
- 🔒 **Security-Focused**: Security audit and vulnerability detection prompts
- 🌍 **Language Support**: Starting with English, expandable to other languages
- 📖 **Well-Documented**: Clear examples and best practices

## Repository Structure

```
prompts/
├── english/
│   ├── agents/                                 # 🆕 Agent-optimized prompts
│   │   ├── claude-agent-system-prompt.md       # Core agent system
│   │   ├── error-analysis-prompt.md            # Debugging specialist
│   │   ├── project-workflow-prompt.md          # Project lifecycle
│   │   ├── agent-quick-reference.md            # Cheat sheet
│   │   ├── code-review-prompt.md               # Code review specialist
│   │   ├── security-audit-prompt.md            # Security audit specialist
│   │   ├── refactoring-prompt.md               # Refactoring specialist
│   │   ├── testing-strategies-prompt.md        # Testing specialist
│   │   ├── documentation-prompt.md             # Documentation specialist
│   │   ├── performance-optimization-prompt.md  # Performance specialist
│   │   ├── git-version-control-prompt.md       # Git & version control
│   │   └── INDEX.md                            # Agent prompts index
│   ├── base/
│   │   └── claude-foundation-prompt.md         # Core system prompt
│   ├── project-types/
│   │   ├── web-development-prompt.md           # Web dev (React, Vue, etc.)
│   │   ├── api-development-prompt.md           # Backend/API development
│   │   ├── data-science-ml-prompt.md           # Data science & ML
│   │   ├── mobile-development-prompt.md        # Mobile (iOS, Android, React Native, Flutter)
│   │   ├── devops-cicd-prompt.md               # DevOps & CI/CD
│   │   ├── database-sql-prompt.md              # Database design & SQL
│   │   └── general-software-development-prompt.md
│   ├── examples/                               # 🆕 Real-world usage examples
│   │   ├── README.md
│   │   ├── rest-api-example.md
│   │   └── debugging-example.md
│   └── workflows/
│       └── iterative-development-guide.md      # Step-by-step workflow guide
├── turkish/                                    # 🆕 Türkçe prompts
│   ├── agents/
│   │   ├── claude-agent-system-prompt-tr.md
│   │   ├── code-review-prompt-tr.md
│   │   └── error-analysis-prompt-tr.md
│   ├── base/
│   │   └── claude-foundation-prompt-tr.md
│   └── INDEX.md
```

## Quick Start

### For AI Coding Agents (Recommended)

1. **Copy the Agent System Prompt**:
   ```
   [Paste content of claude-agent-system-prompt.md]
   ```

2. **Start working**:
   ```
   Analyze this codebase and fix any issues you find.
   ```

3. **The agent will automatically**:
   - Analyze the codebase
   - Create a plan
   - Execute step by step
   - Iterate until optimal

### For Manual Sessions

### 1. Choose Your Prompt

Select based on your project type:

- **Agent System Prompt**: For AI coding agents (Claude Code, Copilot)
- **Foundation Prompt**: Universal best practices for any project
- **Web Development**: Frontend, React, Vue, responsive design
- **API Development**: REST APIs, GraphQL, backend systems
- **Data Science & ML**: Data analysis, machine learning, modeling

### 2. Provide to Claude

Copy the selected prompt and provide it to Claude at the beginning of your session:

```
Please use this system prompt for our development session:

[Paste the content of your chosen prompt here]
```

### 3. Start Development

Claude will now follow:
- Quality standards from the prompt
- Iterative development cycle
- Best practices for your project type
- Proper commit conventions
- Comprehensive error analysis

## Usage Examples

### Example 1: Starting a Web Project

```markdown
I'm starting a React application for an e-commerce store.
Please use the Web Development prompt to guide our development.

Initial requirements:
- Product listing page
- Shopping cart functionality
- User authentication
```

Claude will:
1. Analyze requirements and existing codebase
2. Plan the implementation in small steps
3. Execute each step with testing
4. Iterate based on results
5. Follow React best practices from the prompt

### Example 2: Building an API

```markdown
I need to create a REST API for a blog platform.
Please use the API Development prompt.

Requirements:
- User authentication (JWT)
- CRUD operations for posts
- Comment system
- Rate limiting
```

Claude will:
1. Analyze API requirements
2. Plan endpoint structure and database schema
3. Implement with proper error handling
4. Add comprehensive tests
5. Follow RESTful conventions

### Example 3: ML Model Development

```markdown
I need to build a customer churn prediction model.
Please use the Data Science & ML prompt.

Dataset: customer_data.csv
Target: churn (binary)
Features: 20 customer attributes
```

Claude will:
1. Analyze data quality and characteristics
2. Plan feature engineering approach
3. Implement model pipeline step-by-step
4. Iterate on model performance
5. Follow ML best practices

## What's Included

### Foundation Prompt
The base prompt provides:
- ✅ Iterative development cycle (Analyze → Plan → Execute → Iterate)
- ✅ Commit message standards
- ✅ Error analysis methodology
- ✅ Code quality principles
- ✅ Testing strategies
- ✅ Documentation requirements

### Web Development Prompt
Additional coverage for web projects:
- Component architecture patterns
- Responsive design best practices
- Accessibility (WCAG) standards
- Performance optimization (Core Web Vitals)
- React/Vue/Angular specific guidelines
- Browser compatibility handling

### API Development Prompt
Backend and API specifics:
- RESTful design principles
- HTTP status code usage
- Authentication & authorization patterns
- Input validation & security
- Rate limiting strategies
- Database optimization
- Error handling patterns

### Data Science & ML Prompt
ML and data analysis focus:
- Data quality assessment
- Exploratory data analysis workflow
- Feature engineering best practices
- Model development pipeline
- Experiment tracking
- Avoiding common ML pitfalls
- Model deployment considerations

### Workflow Guide
Step-by-step instructions for:
- How to apply the Analyze-Plan-Execute-Iterate cycle
- Detailed checklist for each phase
- Real-world examples
- When to iterate vs when to stop
- Common pitfalls to avoid

## Prompt Features

### Commit Standards
```
<type>: <description>

<body>

<footer>
```

Types: feat, fix, docs, style, refactor, test, chore

### Error Analysis Process
1. Capture complete context
2. Reproduce consistently
3. Analyze root cause
4. Propose multiple solutions
5. Implement and verify
6. Document and prevent recurrence

### Quality Principles
- Code is read more than written (readability first)
- Make it work, make it right, make it fast (in that order)
- Test continuously, not at the end
- Simple over clever
- DRY (Don't Repeat Yourself)
- SOLID principles

## Customization

You can customize prompts for your team:

1. Fork this repository
2. Modify prompts to match your standards
3. Add team-specific conventions
4. Include your preferred tools/libraries
5. Add company-specific guidelines

Example additions:
```markdown
## Team-Specific Standards

### Our Stack
- Frontend: React 18 with TypeScript
- Backend: Node.js with Express
- Database: PostgreSQL
- Testing: Jest + React Testing Library

### Our Conventions
- Use Tailwind CSS for styling
- Redux Toolkit for state management
- Follow Airbnb style guide
```

## Contributing

We welcome contributions! Areas for contribution:

1. **New Language Support**: Add prompts in other languages
2. **New Project Types**: Add prompts for other domains (mobile, DevOps, etc.)
3. **Improvements**: Enhance existing prompts with better practices
4. **Examples**: Add more real-world usage examples
5. **Tools**: Create tools to help integrate prompts

## Best Practices

### When Using These Prompts

1. **Read the Full Prompt**: Understand the complete system before starting
2. **Start Simple**: Begin with the foundation prompt, add specialization as needed
3. **Trust the Process**: Follow the Analyze-Plan-Execute-Iterate cycle
4. **Validate Continuously**: Test after each change, not at the end
5. **Iterate Purposefully**: Each iteration should have clear improvement goals

### Combining Prompts

You can combine prompts for complex projects:

```markdown
Use the Foundation Prompt as the base.
Additionally, apply Web Development prompt for the frontend
and API Development prompt for the backend.
```

## FAQ

**Q: Which prompt should I use?**
A: For AI coding agents (Claude Code, Copilot), use the **Agent System Prompt**. For manual sessions, start with the **Foundation Prompt** and add project-specific prompts as needed.

**Q: What's the difference between Agent and Foundation prompts?**
A: Agent prompts are token-optimized and designed for autonomous operation. Foundation prompts are more comprehensive and suited for interactive sessions.

**Q: Can I modify the prompts?**
A: Absolutely! These are templates. Customize them for your needs.

**Q: How do I know when to stop iterating?**
A: When success criteria are met and further improvements provide diminishing returns.

**Q: Do these work with other AI models?**
A: They're optimized for Claude but can be adapted for other models like GPT-4, Gemini, etc.

**Q: Can I use these for commercial projects?**
A: Yes! These prompts are provided for use in any project.

## Examples of Optimal Workflows

### Feature Development
```
Day 1 - Iteration 1:
  Analyze → Plan → Execute (basic version) → Evaluate
  Result: Working feature, but performance concerns

Day 2 - Iteration 2:
  Analyze (performance) → Plan (optimization) → Execute → Evaluate
  Result: Meets performance targets, optimal

Total: 2 iterations to optimal
```

### Bug Fix
```
Iteration 1:
  Analyze (reproduce, root cause) → Plan → Execute (fix) → Evaluate
  Result: Bug fixed, but introduced edge case issue

Iteration 2:
  Analyze (edge case) → Plan → Execute → Evaluate
  Result: Bug fixed, all cases handled, optimal

Total: 2 iterations to optimal
```

## License

MIT License - Feel free to use, modify, and distribute.

## Support

For questions, issues, or suggestions:
- Open an issue in this repository
- Submit a pull request with improvements

## Acknowledgments

These prompts are built on:
- Industry best practices
- Software engineering principles
- Agile and iterative development methodologies
- Community feedback and real-world usage

---

**Remember**: The goal is not perfection, but continuous improvement toward optimal solutions. Use these prompts to build better software, faster, with fewer errors.
