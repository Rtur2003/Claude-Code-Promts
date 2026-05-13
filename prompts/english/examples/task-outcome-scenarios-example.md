# Example: Task-to-Outcome Scenario Pack

Use these short scenarios when you need a clear task brief format with measurable outputs.

## Scenario 1: Bug Fix

### Input Task

```text
Production checkout occasionally returns HTTP 500 under peak load.
Identify root cause and deliver a safe fix with verification evidence.
```

### Expected Output Format

```markdown
## Bug Fix Report
### Root Cause
### Fix Plan
### Files/Areas Changed
### Verification Evidence
### Rollback Plan
```

### Success Criteria

- Root cause is confirmed with logs/traces or reproducible steps
- Fix includes validation steps and no behavior regression
- Verification evidence is explicit and repeatable

---

## Scenario 2: Refactor

### Input Task

```text
Refactor a large service module with high complexity while preserving behavior.
```

### Expected Output Format

```markdown
## Refactor Summary
### Baseline Metrics
### Refactor Strategy
### Behavior-Safety Checks
### Post-Refactor Metrics
```

### Success Criteria

- No functional behavior changes
- Complexity or maintainability metrics improve
- Safety checks confirm parity

---

## Scenario 3: Security Review

### Input Task

```text
Run a security review for authentication, authorization, and input validation
for a user-facing API.
```

### Expected Output Format

```markdown
## Security Review Report
### Scope
### Findings by Severity
### Remediation Plan
### Residual Risks
### Verification Plan
```

### Success Criteria

- Findings are severity-ranked and actionable
- Remediation steps are concrete and testable
- Residual risk is explicitly documented

---

## Scenario 4: Migration & Upgrade

### Input Task

```text
Plan and execute a framework upgrade with minimal downtime risk.
```

### Expected Output Format

```markdown
## Migration Report
### Current State
### Target State
### Incremental Rollout Plan
### Compatibility/Validation Checks
### Rollback Strategy
```

### Success Criteria

- Migration plan is incremental and reversible
- Compatibility checks are defined before rollout
- Rollback path is documented and executable

---

## Recommended Prompt Setups

- Bug fix: `Agent System + Debugging & Troubleshooting`
- Refactor: `Agent System + Refactoring`
- Security review: `Agent System + Security Audit`
- Migration: `Agent System + Migration & Upgrade`
