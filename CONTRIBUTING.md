# Contributing

## How to Contribute

| Type | Description |
|------|-------------|
| **New Project Types** | Game dev, blockchain, embedded systems, etc. |
| **New Agent Types** | Architecture review, accessibility audit, etc. |
| **Improvements** | Better practices, clearer instructions, examples |
| **Bug Fixes** | Typos, broken links, formatting issues |

## Quick Setup

```bash
git clone https://github.com/YOUR_USERNAME/Claude-Code-Promts.git
cd Claude-Code-Promts
git checkout -b feature/your-feature-name
```

## File Structure

```
prompts/
└── english/
    ├── agents/           # Agent-optimized prompts
    ├── base/             # Foundation prompts
    ├── project-types/    # Domain-specific prompts
    ├── examples/         # Usage examples
    └── workflows/        # Process guides
```

## Naming Convention

| Type | Format | Example |
|------|--------|---------|
| Prompts | `kebab-case-prompt.md` | `code-review-prompt.md` |
| Guides | `kebab-case-guide.md` | `iterative-development-guide.md` |
| Index | `INDEX.md` | `INDEX.md` |

## Prompt Template

```markdown
# Prompt Title

> **Key Feature 1** | **Key Feature 2** | **Key Feature 3**

## Role
[Define what this prompt does]

## Protocol / Core Loop
[Main workflow]

## Phases
[Phase details with templates and checklists]

## Remember
[Key takeaways]
```

## Checklist Before Submitting

- [ ] Content is accurate and follows best practices
- [ ] Markdown renders correctly
- [ ] No spelling or grammar errors
- [ ] INDEX files updated
- [ ] Links work correctly
- [ ] Follows existing style

## Commit Messages

```bash
feat: add security audit prompt       # New features
fix: correct typo in API prompt        # Fixes
docs: improve README examples          # Documentation
update: enhance code review checklist  # Updates
```

## Pull Request Process

1. Create branch → make changes → commit
2. Push and create PR with clear description
3. Address review feedback
4. Merge after approval

## License

Contributions are licensed under MIT License.

---

Thank you for contributing! 🚀
