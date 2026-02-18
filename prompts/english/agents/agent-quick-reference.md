# Agent Quick Reference Card

> **Token-Optimized Cheat Sheet** | **Copy & Use**

---

## 🔄 Core Loop: APEI

```
A → ANALYZE: What's the problem? What exists?
P → PLAN: Minimal steps to solve?
E → EXECUTE: One step → test → commit
I → ITERATE: Optimal? If not → A
```

---

## 📋 Templates

### Analysis Summary
```markdown
**Problem**: [1 sentence]
**Stack**: [lang/framework]
**Files**: [affected files]
**Success**: [measurable criteria]
```

### Task Plan
```markdown
**Step 1**: [action] → Files: [x,y] → Test: [how]
**Step 2**: [action] → Files: [x,y] → Test: [how]
```

### Error Report
```markdown
**Error**: [type] at [file:line]
**Cause**: [root cause]
**Fix**: [solution]
**Verify**: [test command]
```

### Progress Update
```markdown
✅ Done: [completed tasks]
🔄 Now: [current task]
⏳ Next: [upcoming tasks]
```

---

## 🔧 Claude Code Modes

```
/compact    → Fast, minimal tokens (simple tasks)
/think      → Extended reasoning (complex logic)
/ultrathink → Max depth (architecture, security)
/clear      → Reset context (between tasks)
/cost       → Check token usage
/memory     → View/edit CLAUDE.md
/init       → Initialize project CLAUDE.md
```

### Mode Selection

```
Simple fix/rename    → /compact
Standard feature     → Normal (default)
Complex algorithm    → /think
Critical decision    → /ultrathink
```

---

## 💻 Commands

### Discover Project
```bash
tree -L 3 -I 'node_modules|dist|.git'
cat package.json | head -30
git log --oneline -10
```

### Validate Changes
```bash
# JS/TS
npm test && npm run lint && npm run build

# Python
pytest && flake8 && mypy .

# Go
go test ./... && golangci-lint run
```

### Git Workflow
```bash
git checkout -b feature/name
# make changes
npm test
git add . && git commit -m "type(scope): msg"
git push
```

---

## ✍️ Commit Format

```
type(scope): description

[optional body]

[optional footer]
```

**Types**: `feat` `fix` `refactor` `test` `docs` `perf` `chore`

**Examples**:
```
feat(auth): add JWT refresh tokens
fix(api): handle null response gracefully
test(user): add edge case coverage
```

---

## ⚡ Priority Matrix

```
┌────────────────┬────────────────┐
│ HIGH IMPACT    │ HIGH IMPACT    │
│ LOW EFFORT     │ HIGH EFFORT    │
│ → DO FIRST     │ → PLAN WELL    │
├────────────────┼────────────────┤
│ LOW IMPACT     │ LOW IMPACT     │
│ LOW EFFORT     │ HIGH EFFORT    │
│ → DO IF TIME   │ → SKIP         │
└────────────────┴────────────────┘
```

---

## ✅ Checklists

### Before Commit
- [ ] Tests pass
- [ ] Lint passes
- [ ] No debug statements
- [ ] Build succeeds

### Error Fix
- [ ] Root cause found
- [ ] Fix applied
- [ ] Test added
- [ ] Verified working

### Feature Complete
- [ ] Acceptance criteria met
- [ ] Tests added
- [ ] Docs updated
- [ ] Reviewed

---

## 🎯 Quality Principles

```
Readable > Clever
Tested > Assumed
Simple > Complex
Explicit > Implicit
Consistent > Personal
```

---

## 🔧 Debug Workflow

```
1. Capture: Error message + stack trace
2. Reproduce: Minimal steps to trigger
3. Isolate: Find exact failing line
4. Fix: Apply minimal change
5. Verify: Run tests + manual check
6. Prevent: Add regression test
```

---

## 📊 Common Patterns

### API Response
```json
{"success": true, "data": {...}}
{"success": false, "error": {"code": "X", "message": "Y"}}
```

### Error Handling
```javascript
try {
  await operation();
} catch (error) {
  logger.error('Operation failed', { error });
  throw new AppError('Failed', 500);
}
```

### Test Structure
```javascript
describe('Feature', () => {
  it('should handle happy path', () => {
    // arrange → act → assert
  });
  it('should handle error case', () => {
    // arrange → act → assert error
  });
});
```

---

## 🚀 Quick Wins

| Issue | Solution |
|-------|----------|
| Slow builds | Enable caching |
| Flaky tests | Add retries / fix async |
| Large bundle | Code splitting |
| N+1 queries | Use joins / eager load |
| Memory leaks | Check event listeners |

---

## 📝 When Stuck

1. **Simplify**: Remove complexity until it works
2. **Isolate**: Create minimal reproduction
3. **Log**: Add debug output at key points
4. **Search**: Check error message online
5. **Ask**: Describe what you've tried

---

> **Remember**: Progress over perfection. Iterate to optimal.
