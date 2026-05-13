# Contributing

## Scope

This repository is **English-only** and **Markdown-only**.

## How to Contribute

| Type | Description |
|------|-------------|
| New prompts | Agent, project-type, or workflow prompts |
| Improvements | Better structure, clarity, outcome quality |
| Examples | Real-world APEI walkthroughs |
| Maintenance | Link fixes, catalog cleanup, archive actions |

## Prompt Quality Standard

Every prompt must contain:
- `## Role`
- `## Protocol / Core Loop`
- `## Phases`
- `## Remember` (final section)

### No Vague Advice Rule

Every recommendation should end with a concrete:
- decision, or
- tool, or
- validation step.

Use this measurable checklist for prompt reviews:
- [Prompt Review Checklist](prompts/english/workflows/prompt-review-checklist.md)

## Archive Workflow

If a prompt is low-value or overlapping:
1. Classify as keep / merge / archive
2. Move to `prompts/english/agents/archive/`
3. Update active indexes and README
4. Add rationale to archive index

## Required PR Checklist

Copy this checklist into your PR description and complete all items:

- [ ] Markdown renders correctly
- [ ] No spelling or grammar errors
- [ ] Internal relative links resolve
- [ ] Hypothetical example paths are plain code literals (not Markdown links)
- [ ] Catalog/index entries are updated
- [ ] `llms.txt` is updated when primary navigation or core prompts change
- [ ] No vague advice language
- [ ] Prompt changes pass `Role / Protocol / Phases / Remember` review checklist
- [ ] Navigation consistency checked across `README.md`, `prompts/english/INDEX.md`, `prompts/english/agents/INDEX.md`, and `llms.txt`
- [ ] Markdown lint passed: `npx markdownlint-cli2 '**/*.md'`

Optional local checks:

```bash
grep -r '\[.*\](.*\.md)' prompts/ | head
npx markdownlint-cli2 '**/*.md'
```

## Commit Message Style

```text
feat: add new prompt
fix: correct catalog link
docs: improve usage guidance
update: archive overlapping prompt
```
