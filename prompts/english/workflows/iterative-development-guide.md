# Iterative Development Workflow

## Overview
This guide demonstrates how to apply the **Analyze → Plan → Execute → Iterate** cycle to achieve optimal results in software development.

## The Core Cycle

```
     ┌──────────────┐
     │   ANALYZE    │ ← Return here if not optimal
     │ Understand   │
     │  Problem     │
     └──────┬───────┘
            ↓
     ┌──────────────┐
     │     PLAN     │
     │  Design      │
     │  Solution    │
     └──────┬───────┘
            ↓
     ┌──────────────┐
     │   EXECUTE    │
     │ Implement    │
     │ Step by Step │
     └──────┬───────┘
            ↓
     ┌──────────────┐
     │   EVALUATE   │
     │  Measure &   │
     │  Review      │
     └──────┬───────┘
            ↓
        Optimal? ─No─→ Back to ANALYZE
            ↓
           Yes
            ↓
          DONE
```

## Phase 1: Analyze

### Objectives
- Fully understand the problem or requirement
- Gather all necessary context
- Identify constraints and dependencies
- Assess current state

### Activities

#### 1. Requirements Analysis
```markdown
Questions to answer:
- What is the goal?
- What are the acceptance criteria?
- What are the constraints (time, resources, technical)?
- Who are the stakeholders?
- What is the expected timeline?
```

#### 2. Codebase Analysis
```bash
# Explore repository structure
tree -L 3 -I 'node_modules|dist|build'

# Review recent changes
git log --oneline -20

# Check current status
git status

# Review existing tests
npm test --listTests # or equivalent

# Check dependencies
npm list --depth=0 # or pip list, etc.
```

#### 3. Technical Assessment
- Review existing architecture
- Identify design patterns in use
- Understand testing approach
- Check CI/CD setup
- Review documentation

#### 4. Risk Identification
Common risks to consider:
- Breaking existing functionality
- Performance degradation
- Security vulnerabilities
- Backwards compatibility issues
- Integration problems
- Technical debt increase

### Analysis Checklist
- [ ] Requirements clearly understood
- [ ] Codebase structure mapped out
- [ ] Existing patterns identified
- [ ] Dependencies documented
- [ ] Test coverage assessed
- [ ] Risks identified
- [ ] Constraints noted
- [ ] Success criteria defined

### Analysis Output
Document your findings:
```markdown
## Analysis Summary

### Problem Statement
[Clear description of what needs to be done]

### Current State
[What exists now]

### Constraints
- [List any limitations]

### Dependencies
- [List dependencies and integrations]

### Risks
1. [Risk 1]: Mitigation: [how to address]
2. [Risk 2]: Mitigation: [how to address]

### Success Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
```

## Phase 2: Plan

### Objectives
- Design the solution
- Break work into manageable steps
- Prioritize tasks
- Define validation approach

### Activities

#### 1. Solution Design
Consider multiple approaches:
```markdown
## Approach A: [Name]
Pros:
- [Advantage 1]
- [Advantage 2]

Cons:
- [Disadvantage 1]
- [Disadvantage 2]

## Approach B: [Name]
Pros:
- [Advantage 1]

Cons:
- [Disadvantage 1]

## Selected Approach: [A or B]
Rationale: [Why this approach is best]
```

#### 2. Task Breakdown
Break the work into small, testable units:
```markdown
## Implementation Plan

### Phase 1: Foundation
- [ ] Task 1.1: [Small, specific task]
  - Estimated time: [X minutes]
  - Validation: [How to test]
- [ ] Task 1.2: [Small, specific task]
  - Estimated time: [X minutes]
  - Validation: [How to test]

### Phase 2: Core Implementation
- [ ] Task 2.1: [Small, specific task]
- [ ] Task 2.2: [Small, specific task]

### Phase 3: Integration & Testing
- [ ] Task 3.1: Integration tests
- [ ] Task 3.2: E2E tests
- [ ] Task 3.3: Performance testing

### Phase 4: Documentation
- [ ] Update README
- [ ] Update API docs
- [ ] Add code comments
```

#### 3. Testing Strategy
Define how each change will be validated:
```markdown
## Testing Plan

### Unit Tests
- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]

### Integration Tests
- [ ] Test scenario 1: [Description]
- [ ] Test scenario 2: [Description]

### Manual Validation
- [ ] Step 1: [Action to take]
  - Expected: [What should happen]
- [ ] Step 2: [Action to take]
  - Expected: [What should happen]
```

### Planning Checklist
- [ ] Solution approach selected
- [ ] Work broken into small tasks
- [ ] Tasks ordered by dependency
- [ ] Each task has validation criteria
- [ ] Testing strategy defined
- [ ] Rollback plan considered
- [ ] Documentation needs identified

### Planning Output
A detailed, actionable plan:
```markdown
## Execution Plan

### Overview
[Brief description of solution]

### Steps (in order)
1. [Step 1]: [What to do]
   - Files: [Files to modify]
   - Tests: [Tests to add/update]
   - Validation: [How to verify]

2. [Step 2]: [What to do]
   - Files: [Files to modify]
   - Tests: [Tests to add/update]
   - Validation: [How to verify]

### Rollback Plan
If things go wrong:
1. [Rollback step 1]
2. [Rollback step 2]
```

## Phase 3: Execute

### Objectives
- Implement the plan step by step
- Validate each change immediately
- Adapt plan based on learnings
- Maintain quality throughout

### Activities

#### 1. Setup Environment
```bash
# Ensure clean starting state
git status

# Create feature branch if needed
git checkout -b feature/descriptive-name

# Install/update dependencies
npm install # or pip install -r requirements.txt
```

#### 2. Implement Step by Step

For each task in the plan:

**Step Template:**
```markdown
## Task: [Task Name]

### Implementation
1. [Action 1]
2. [Action 2]
3. [Action 3]

### Validation
```bash
# Run relevant tests
npm test path/to/test

# Manual verification
[Commands to verify change works]
```

### Commit
```bash
git add [files]
git commit -m "feat: [clear description]

[Body explaining why and how]

Relates to #[issue number]"
```

### Review
- Does it work as expected?
- Are tests passing?
- Is code quality maintained?
- Any unexpected side effects?
```

#### 3. Continuous Validation

After EACH change:
```bash
# Run related tests
npm test -- path/to/changed/area

# Run linter
npm run lint

# Check for type errors (if applicable)
npm run type-check

# Manual smoke test
# [Run the application and verify]
```

#### 4. Documentation as You Go

Update documentation with each change:
- Add code comments for complex logic
- Update README if behavior changes
- Update API docs if interface changes
- Add inline examples where helpful

### Execution Checklist (per task)
- [ ] Task implemented
- [ ] Tests added/updated
- [ ] Tests passing
- [ ] Linting passing
- [ ] Manual verification done
- [ ] Documentation updated
- [ ] Code reviewed (self-review)
- [ ] Committed with clear message

### Execution Best Practices

#### Make Small, Atomic Commits
```bash
# ✅ GOOD: Small, focused commits
git commit -m "feat: add user validation"
git commit -m "test: add user validation tests"
git commit -m "docs: update user API docs"

# ❌ BAD: Giant, unfocused commit
git commit -m "implement entire feature with tests and docs"
```

#### Validate Continuously
```bash
# After each file change
npm test -- path/to/test.js

# Before each commit
npm test && npm run lint && git commit
```

#### Keep Changes Reversible
```bash
# If something goes wrong
git diff  # Review changes
git checkout -- file.js  # Revert single file
git reset --hard  # Revert all changes (last resort)
```

## Phase 4: Evaluate

### Objectives
- Measure results against success criteria
- Identify what worked well
- Identify what needs improvement
- Decide if another iteration is needed

### Activities

#### 1. Test Full Integration
```bash
# Run complete test suite
npm test

# Run E2E tests
npm run test:e2e

# Check code coverage
npm run test:coverage

# Performance tests (if applicable)
npm run test:performance
```

#### 2. Quality Checks
```bash
# Code quality
npm run lint
npm run type-check

# Security scan
npm audit

# Bundle size (for web)
npm run build
ls -lh dist/
```

#### 3. Manual Verification
Test the actual user experience:
```markdown
## Manual Test Checklist
- [ ] Happy path works
- [ ] Error cases handled gracefully
- [ ] Edge cases covered
- [ ] Performance acceptable
- [ ] UI/UX smooth (if applicable)
- [ ] Backwards compatible
- [ ] No regressions in existing features
```

#### 4. Review Against Success Criteria
```markdown
## Success Criteria Review

Original criteria:
- [ ] Criterion 1: [Status and notes]
- [ ] Criterion 2: [Status and notes]
- [ ] Criterion 3: [Status and notes]

All criteria met? [Yes/No]
If No, what's missing? [Description]
```

#### 5. Identify Improvements
```markdown
## What Worked Well
- [Thing 1]
- [Thing 2]

## What Could Be Better
- [Improvement 1]
- [Improvement 2]

## Should We Iterate?
- [ ] No - Solution is optimal for current needs
- [ ] Yes - [Specific improvements needed]
```

### Evaluation Checklist
- [ ] All tests passing
- [ ] Code quality checks passed
- [ ] Manual testing completed
- [ ] Success criteria reviewed
- [ ] Performance measured
- [ ] Security checked
- [ ] Documentation complete
- [ ] Improvement opportunities identified

### Evaluation Output

#### Decision: Continue to Next Iteration
If improvements are needed:
```markdown
## Iteration N+1 Plan

### Issues Found
1. [Issue 1]: [Description]
2. [Issue 2]: [Description]

### Proposed Improvements
1. [Improvement 1]: [Expected benefit]
2. [Improvement 2]: [Expected benefit]

### Next Steps
Return to ANALYZE phase with new focus:
[What to analyze in next iteration]
```

#### Decision: Complete
If solution is optimal:
```markdown
## Completion Summary

### Achievements
- [Achievement 1]
- [Achievement 2]

### Metrics
- Test coverage: [X%]
- Performance: [metrics]
- Code quality: [metrics]

### Lessons Learned
- [Lesson 1]
- [Lesson 2]

### Future Considerations
- [Potential enhancement 1]
- [Potential enhancement 2]
```

## Real-World Example

### Scenario
Add authentication to an existing API

### Iteration 1

#### Analyze
- Current state: API has no authentication
- Goal: Add JWT-based authentication
- Constraints: Don't break existing clients initially
- Risk: Existing integrations might break

#### Plan
1. Add authentication middleware (optional initially)
2. Create login endpoint
3. Add tests
4. Update documentation
5. Make authentication required (phase 2)

#### Execute
```bash
# Step 1: Install dependencies
npm install jsonwebtoken bcrypt

# Step 2: Create auth middleware
# [Implement auth.middleware.js]
npm test auth.middleware.test.js ✓

# Step 3: Create login endpoint
# [Implement auth.controller.js]
npm test auth.controller.test.js ✓

# Step 4: Add to existing routes (optional)
# [Update routes with optional auth]
npm test ✓

git commit -m "feat(auth): add JWT authentication"
```

#### Evaluate
- ✓ Authentication works
- ✓ Tests pass
- ✓ Existing clients still work (auth optional)
- ⚠️  Performance concern: Token verification on every request
- → **Decision**: Iterate to add caching

### Iteration 2

#### Analyze
- Issue: Token verification is slow (100ms per request)
- Goal: Reduce to <10ms
- Approach: Add Redis caching for verified tokens

#### Plan
1. Add Redis caching layer
2. Cache verified tokens (5 min TTL)
3. Benchmark performance
4. Update documentation

#### Execute
```bash
npm install redis
# [Implement token caching]
npm test ✓
# Benchmark: Token verification now 5ms ✓
git commit -m "perf(auth): add Redis caching for token verification"
```

#### Evaluate
- ✓ Performance target met
- ✓ All tests pass
- ✓ Documentation updated
- → **Decision**: Solution is optimal, complete

## Tips for Effective Iteration

### When to Iterate
- Success criteria not fully met
- Performance issues discovered
- Edge cases found
- Better approach identified
- New requirements emerged

### When to Stop
- All success criteria met
- Diminishing returns on improvements
- Time/resource constraints
- Good enough for current needs

### Signs of Good Iteration
- Each iteration adds value
- Changes are measurable
- Learning from previous iterations
- Clear progress toward goal

### Signs of Poor Iteration
- Circular changes (undoing previous work)
- No measurable improvement
- Scope creep
- Changes based on assumptions, not data

## Remember

- **Iterate with purpose**: Each iteration should have clear goals
- **Measure progress**: Use metrics to track improvement
- **Know when to stop**: Perfect is the enemy of done
- **Document learnings**: Help future iterations

The goal is not infinite iteration, but reaching an optimal solution efficiently.
