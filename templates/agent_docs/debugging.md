# Debugging Procedures

> This document describes the systematic debugging approach for this project.

## Debugging Workflow

```
1. REPRODUCE → Confirm the bug exists
2. ISOLATE   → Find the smallest failing case
3. ANALYZE   → Understand root cause
4. FIX       → Make minimal change
5. VERIFY    → Confirm fix works
6. TEST      → Add regression test
```

## Reproduction Steps

```markdown
### Bug Report Template

**Symptom**: What you observe
**Expected**: What should happen
**Steps to Reproduce**:
1. Step one
2. Step two
3. ...

**Environment**:
- OS:
- Version:
- Config:
```

## Isolation Techniques

### Binary Search
```bash
# Find which commit introduced the bug
git bisect start
git bisect bad HEAD
git bisect good <last-known-good-commit>
# Git will guide through commits
```

### Minimal Reproduction
```python
# Reduce to smallest failing case
def test_minimal_reproduction():
    # Remove all unnecessary code
    # until bug still reproduces
    assert broken_function(minimal_input) == expected
```

## Analysis Tools

```bash
# View logs
tail -f logs/app.log

# Check stack trace
python -c "import traceback; traceback.print_exc()"

# Debugger
python -m pdb script.py

# Interactive debugging
import pdb; pdb.set_trace()
```

## Fix Guidelines

1. **Minimal Change**: Fix only the bug, no refactoring
2. **Root Cause**: Fix the cause, not the symptom
3. **No Workarounds**: Proper fix, not hacks

## Verification Checklist

- [ ] Bug is fixed
- [ ] Tests pass
- [ ] No regressions introduced
- [ ] Regression test added
- [ ] Documentation updated (if needed)

## Common Issues

| Symptom | Likely Cause | Debug Step |
|---------|--------------|------------|
| Import error | Missing dependency | `pip list` |
| Type error | Wrong type passed | Add type hints |
| Null error | Missing validation | Add guard clause |
| Timeout | Slow operation | Profile code |

## Escalation

If unable to resolve within 30 minutes:
1. Document what you've tried
2. Create minimal reproduction
3. Ask for help with specific question
