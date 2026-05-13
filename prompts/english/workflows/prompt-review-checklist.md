# Prompt Review Checklist

Use this checklist for periodic prompt quality reviews.

---

## Review Cadence

- Monthly: review recently edited prompts
- Quarterly: review all active prompts in `prompts/english/agents/`

---

## Mandatory Structure Check

- [ ] `## Role` exists
- [ ] `## Protocol / Core Loop` exists
- [ ] `## Phases` exists with actionable checklists
- [ ] `## Remember` exists and is the final section

---

## No Vague Advice Check

For each recommendation in the prompt:

- [ ] Ends with a concrete decision, or
- [ ] Names a concrete tool, or
- [ ] Includes a concrete validation step

Fail the review if a recommendation is generic without an action.

---

## Outcome & Clarity Check

- [ ] Prompt scope is explicit (what it should and should not do)
- [ ] Steps are ordered and executable
- [ ] Success criteria are measurable
- [ ] Internal links resolve

---

## Review Result Template

```markdown
## Prompt Review Result

**Prompt**: `<path>`
**Decision**: keep / update / merge / archive

### Structure
- Role: pass/fail
- Protocol: pass/fail
- Phases: pass/fail
- Remember final: pass/fail

### No Vague Advice
- Pass/Fail
- Notes:

### Required Actions
1. ...
2. ...
```
