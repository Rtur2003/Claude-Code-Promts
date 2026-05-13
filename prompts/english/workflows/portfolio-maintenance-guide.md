# Prompt Portfolio Maintenance Guide

> **Outcome-First** | **Low-Friction Selection** | **90-Day Governance**

## Role

Maintain a high-signal prompt portfolio that prioritizes execution outcomes over prompt count.

## Protocol: REVIEW

- **R**ecord usage and outcomes
- **E**valuate overlap and drift
- **V**alidate quality gates
- **I**mplement keep/merge/archive actions
- **E**xecute documentation updates
- **W**ork in 90-day cycles

## Operating Cadence

### Monthly Review (Lightweight)

- [ ] Review most-used prompts and top combinations
- [ ] Check whether prompt descriptions still match real usage
- [ ] Update token counts if materially changed
- [ ] Fix stale links in catalog and setup docs

### Quarterly Review (Structural)

- [ ] Reclassify all agent prompts: keep / merge / archive
- [ ] Move archived prompts out of active catalog
- [ ] Update README, prompt indexes, and quick-start mappings
- [ ] Remove or merge low-value duplicate guidance
- [ ] Enforce a forced decision for every prompt (no “undecided” status)

## Forced Decision Rules (Quarterly)

Every active prompt must end the quarterly review with exactly one decision:

- **keep**: unique value and active usage
- **merge**: overlapping guidance better combined with another active prompt
- **archive**: low usage, low differentiation, or outdated scope

If overlap is detected and no clear differentiation exists, default to **merge**.

## Portfolio Decision Log Template

Use concise, comparative rationale so decisions are traceable:

| Prompt | Decision | Compare Against | One-line Rationale | Action |
|--------|----------|-----------------|--------------------|--------|
| `example-prompt.md` | keep | `other-prompt.md` | Higher signal for incident response with lower token cost | Keep in active index |
| `legacy-prompt.md` | merge | `newer-prompt.md` | Duplicates workflow with weaker validation language | Merge and deprecate |
| `old-prompt.md` | archive | `replacement-prompt.md` | Superseded by active prompt with clearer quality gate | Move to archive |

## Quality Gate (Mandatory)

Every active prompt must have:
- [ ] `## Role`
- [ ] `## Protocol / Core Loop` (or equivalent protocol section)
- [ ] `## Phases` with actionable checklists
- [ ] `## Remember` as final section
- [ ] Outcome-focused language with no vague advice

## No Vague Advice Rule

Each recommendation must end with one of:
- A concrete decision
- A concrete tool
- A concrete validation step

Example:
- Vague: "Improve performance and keep it reliable."
- Outcome-focused: "Run EXPLAIN ANALYZE on the slow query, add a composite index on `(user_id, created_at)`, and verify p95 latency is below 120ms."

## Success Metrics

- Fewer prompts in active catalog without capability loss
- Faster prompt selection from README and indexes
- Higher task completion rate with fewer follow-up clarifications

## Remember

Prioritize measurable outcomes. If a prompt does not improve decisions or execution quality, merge it or archive it.
