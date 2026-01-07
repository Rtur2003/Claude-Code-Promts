# Contributing to Claude Code Prompts

Thank you for your interest in contributing to Claude Code Prompts! This document provides guidelines and instructions for contributing.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Contribution Guidelines](#contribution-guidelines)
- [Pull Request Process](#pull-request-process)
- [Style Guide](#style-guide)
- [Community](#community)

## Code of Conduct

This project follows a Code of Conduct to ensure a welcoming environment for all contributors. Please be respectful, inclusive, and professional in all interactions.

## How Can I Contribute?

### 🐛 Reporting Issues

If you find a problem with any prompt:

1. **Search existing issues** to avoid duplicates
2. **Create a new issue** with:
   - Clear title describing the problem
   - Which prompt file is affected
   - Description of the issue
   - Expected vs actual behavior
   - Suggestions for improvement (if any)

### 💡 Suggesting Enhancements

Have an idea for a new prompt or improvement?

1. **Check existing issues and prompts** for similar ideas
2. **Open a discussion** or issue with:
   - Clear description of the enhancement
   - Use cases and benefits
   - Examples if applicable

### 📝 Creating New Prompts

We welcome new prompts! Areas where contributions are especially valuable:

- **New Languages**: Turkish, Spanish, German, French, etc.
- **New Project Types**: Game development, embedded systems, blockchain, etc.
- **New Agent Types**: Documentation specialist, architecture review, etc.
- **Improvements**: Better practices, clearer instructions, more examples

### 🔧 Improving Existing Prompts

Even small improvements help:

- Fix typos and grammar
- Clarify confusing sections
- Add missing examples
- Update outdated practices
- Improve formatting

## Development Setup

### Prerequisites

- Git installed
- Markdown editor (VS Code recommended)
- Basic understanding of the prompt types in this repository

### Local Setup

```bash
# Fork the repository on GitHub
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/Claude-Code-Promts.git
cd Claude-Code-Promts

# Create a branch for your changes
git checkout -b feature/your-feature-name
```

## Contribution Guidelines

### Creating a New Prompt

1. **Choose the right location**:
   ```
   prompts/
   ├── english/
   │   ├── agents/           # Agent-optimized prompts
   │   ├── base/             # Foundation prompts
   │   ├── project-types/    # Domain-specific prompts
   │   └── workflows/        # Process guides
   └── [language]/           # Non-English prompts
   ```

2. **Use consistent naming**:
   - Use kebab-case: `code-review-prompt.md`
   - Be descriptive: `security-audit-prompt.md`
   - Include `-prompt` suffix for prompts

3. **Follow the template structure**:
   ```markdown
   # Prompt Title
   
   > **Key Feature 1** | **Key Feature 2** | **Key Feature 3**
   
   ## Role / Overview
   [Define what this prompt does]
   
   ## Core Foundation
   [Link to foundation prompt if applicable]
   
   ## Main Content
   [The actual prompt content]
   
   ## Examples
   [Practical examples]
   
   ## Remember
   [Key takeaways]
   ```

4. **Update INDEX files**:
   - Add entry to `prompts/english/INDEX.md`
   - Add entry to `prompts/english/agents/INDEX.md` (if agent prompt)
   - Update `README.md` if adding a new category

### Adding a New Language

1. **Create language folder**: `prompts/[language-code]/`
2. **Mirror the English structure**:
   ```
   prompts/
   └── turkish/              # Or: spanish, german, etc.
       ├── agents/
       ├── base/
       ├── project-types/
       ├── workflows/
       └── INDEX.md
   ```
3. **Translate prompts** maintaining technical accuracy
4. **Update main README** to list the new language

### Quality Checklist

Before submitting:

- [ ] Content is accurate and follows best practices
- [ ] Markdown renders correctly
- [ ] No spelling or grammar errors
- [ ] Examples are working and realistic
- [ ] Follows existing style and formatting
- [ ] INDEX files updated
- [ ] Links work correctly

## Pull Request Process

### 1. Create Your Branch

```bash
git checkout -b feature/add-security-prompt
# or
git checkout -b fix/typo-in-api-prompt
# or
git checkout -b docs/improve-readme
```

### 2. Make Your Changes

- Keep changes focused (one feature/fix per PR)
- Test your markdown renders correctly
- Verify all links work

### 3. Commit Your Changes

Use conventional commits:

```bash
# For new features
git commit -m "feat: add security audit prompt"

# For fixes
git commit -m "fix: correct typo in API prompt"

# For documentation
git commit -m "docs: improve README examples"

# For updates
git commit -m "update: enhance code review checklist"
```

### 4. Push and Create PR

```bash
git push origin your-branch-name
```

Then create a Pull Request on GitHub with:

- Clear title describing the change
- Description of what and why
- Link to related issues (if any)
- Screenshots for visual changes

### 5. Review Process

- Maintainers will review your PR
- Address any requested changes
- Once approved, your PR will be merged

## Style Guide

### Markdown Formatting

```markdown
# H1 - Document Title
## H2 - Major Sections
### H3 - Subsections
#### H4 - Details

**Bold** for emphasis
`code` for inline code
```code block``` for code examples

- Use bullet lists for unordered items
1. Use numbered lists for sequential items

| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |

> Blockquotes for important notes
```

### Code Examples

- Use appropriate language tags for syntax highlighting
- Keep examples concise but complete
- Include comments explaining complex parts
- Test that examples actually work

### Writing Style

- Be clear and concise
- Use active voice
- Explain "why" not just "what"
- Include practical examples
- Maintain consistent terminology

### Checklist Format

```markdown
- [ ] Unchecked item
- [x] Checked item
```

## File Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Prompts | kebab-case with -prompt suffix | `code-review-prompt.md` |
| Guides | kebab-case with -guide suffix | `iterative-development-guide.md` |
| Index | ALL CAPS | `INDEX.md` |
| Other docs | ALL CAPS or kebab-case | `README.md`, `CONTRIBUTING.md` |

## Community

### Getting Help

- Open a Discussion on GitHub for questions
- Tag issues appropriately
- Be patient and respectful

### Recognition

Contributors are valued! We maintain a list of contributors and appreciate all contributions, big or small.

## License

By contributing, you agree that your contributions will be licensed under the same license as the project (MIT License).

---

Thank you for contributing to Claude Code Prompts! Your efforts help developers worldwide write better code with AI assistance. 🚀
