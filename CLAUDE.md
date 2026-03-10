# CLAUDE.md

## Project Overview
- **Name**: Claude Code Prompts
- **Type**: Prompt library (pure Markdown, no code)
- **Purpose**: Production-ready system prompts for Claude AI coding agents
- **Core Methodology**: APEI cycle — Analyze → Plan → Execute → Iterate
- **License**: MIT
- **Language**: English only

## Repository Structure

```
├── CLAUDE.md              # This file — project memory for Claude Code
├── README.md              # Main documentation with prompt catalog
├── QUICK-START.md         # 30-second setup guide
├── USAGE.md               # Detailed examples & advanced usage
├── CONTRIBUTING.md        # Contribution guidelines
├── CHANGELOG.md           # Version history
└── prompts/
    └── english/
        ├── INDEX.md           # All prompts organized by category
        ├── agents/            # Agent-optimized prompts (28 files)
        │   └── INDEX.md
        ├── base/              # Foundation prompt (universal best practices)
        ├── project-types/     # Domain-specific prompts (11 files: web, API, ML, mobile, blockchain, desktop, etc.)
        ├── examples/          # Real-world usage examples (7 files)
        └── workflows/         # APEI methodology, prompt selection & troubleshooting guides
```

## File Naming Conventions

| Type | Format | Example |
|------|--------|---------|
| Prompts | `kebab-case-prompt.md` | `code-review-prompt.md` |
| Guides | `kebab-case-guide.md` | `iterative-development-guide.md` |
| Index files | `INDEX.md` | `INDEX.md` |

## Prompt Structure Standards

Every prompt follows this template:

```markdown
# Prompt Title

> **Key Feature 1** | **Key Feature 2** | **Key Feature 3**

## Role
[Define what this prompt does]

## Protocol / Core Loop
[Main workflow — often uses a protocol acronym]

## Phases
[Phase details with templates and checklists]

## Remember
[Key takeaways — always the final section]
```

Key elements:
- **Protocol acronym**: Each prompt defines a memorable acronym for its core loop
- **Phases**: Detailed steps with Markdown templates and `- [ ]` checklists
- **Tables**: Used for options, comparisons, and structured data
- **Code blocks**: Used for command examples, templates, and diagrams
- **Remember section**: Closing callout with priority rules (always last)

## Markdown Style Guide

- Use `#` for title, `##` for major sections, `###` for subsections
- Tables for structured data (catalogs, options, comparisons)
- `> **bold text**` for callout/subtitle lines under the title
- Fenced code blocks with language tags where applicable
- `- [ ]` checklists inside phases
- `---` horizontal rules to separate major sections
- Keep prompts concise — include token count in catalog tables
- Use `⭐` emoji only for recommended/primary prompts in catalogs

## Build & Development

No build system — this is a pure Markdown repository.

- **Install**: `git clone` the repo
- **Validate links**: `grep -r '\[.*\](.*\.md)' prompts/ | head` — spot-check relative links
- **Validate formatting**: Open `.md` files in a Markdown previewer
- **Lint (optional)**: `npx markdownlint-cli2 '**/*.md'` if available

## Common Tasks

### Add a new agent prompt
1. Create `prompts/english/agents/your-topic-prompt.md` using the template above
2. Update `prompts/english/agents/INDEX.md` with a new table row
3. Update `prompts/english/INDEX.md`
4. Add entry to the prompt catalog table in `README.md`

### Add a new project-type prompt
1. Create `prompts/english/project-types/your-domain-prompt.md`
2. Update `prompts/english/INDEX.md`
3. Add entry to the Foundation & Project Prompts table in `README.md`
4. Add relevant combinations to the Common Combinations table in `README.md`

### Add a usage example
1. Create a new file in `prompts/english/examples/`
2. Show real-world prompt usage with context and expected output

### Update documentation
1. Edit the relevant `.md` file
2. Ensure all relative links still resolve
3. Keep `CHANGELOG.md` updated for notable changes

## Quality Checklist

Before submitting changes:
- [ ] Content is accurate and follows best practices
- [ ] Markdown renders correctly (check headers, tables, code blocks)
- [ ] No spelling or grammar errors
- [ ] INDEX files updated if adding/removing prompts
- [ ] All relative links resolve to existing files
- [ ] Follows existing naming conventions (`kebab-case-prompt.md`)
- [ ] New prompts include Role, Protocol, Phases, and Remember sections
- [ ] README.md catalog tables updated if adding new prompts

## Commit Messages

```
feat: add security audit prompt       # New features
fix: correct typo in API prompt        # Fixes
docs: improve README examples          # Documentation
update: enhance code review checklist  # Updates
```

## Things to Avoid

- Don't add non-English content — this repo is English only
- Don't add code or build tooling — keep it pure Markdown
- Don't deviate from the APEI methodology in prompt design
- Don't remove the Remember section from prompts
- Don't use absolute URLs for internal links — use relative paths
