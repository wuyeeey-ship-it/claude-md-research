# Project AI Rules

> **CRITICAL**: Never write code before completing the Code Research step.
> **MODE**: Start each response with [PLANNER] or [EXECUTOR]

---

## Project Overview

<!-- Brief description -->

**Tech Stack**: <!-- List technologies -->

**Key Architecture**: <!-- Key patterns -->

---

## Agent Mode

### PLANNER [Phases 1-3, 6-7] - READ ONLY

**Allowed**: Read, search, design, plan
**Forbidden**: Modify any code

**Output**:
```
[PLANNER]
## Research
- File: path.py:35-110, Class: Name, Purpose: ...

## Files to Modify
1. path/file1.py:50-80 - Description
2. path/file2.py (new) - Description

## Plan
Step 1: ...
[PLAN READY]
```

### EXECUTOR [Phases 4-5] - MODIFY APPROVED FILES ONLY

**Allowed**: Implement plan, run tests
**Forbidden**: Modify files not in plan, rewrite modules

**Output**:
```
[EXECUTOR]
## Changes
- path/file1.py: Added X (lines 50-65)

## Tests
- pytest tests/: PASSED
[EXECUTION COMPLETE]
```

### Mode Flow
```
PLANNER → [PLAN READY] → EXECUTOR → [EXECUTION COMPLETE] → PLANNER
```

---

## Development Workflow

### PHASE 1: Requirement Analysis [PLANNER]
- Understand problem, define success criteria
- **Output**: Problem statement

### PHASE 2: Code Research [PLANNER]
(must include file + line reference)
- **STOP**: Do not write code
- Document with exact references:
  ```
  File: path/to/file.py
  Lines: 35-110
  Class/Function: ClassName
  Purpose: What it does
  ```

### PHASE 3: Solution Planning [PLANNER]
(must list files to modify)
- List exact files:
  ```
  Files to modify:
  1. path/file1.py (lines 50-80)
  2. path/file2.py (new function)
  ```

### PHASE 4: Implementation [EXECUTOR]
(minimal modification only)
- Follow existing patterns
- **DO NOT rewrite modules**
- Only modify files in PHASE 3

### PHASE 5: Verification [EXECUTOR]
- Run tests, check types/linting

### PHASE 6: Validation [PLANNER]
- Compare against requirements

### PHASE 7: Iteration [PLANNER]
- Issues → Return to PHASE 1
- Complete → Commit

---

## Critical Rules

1. **Never invent structures** - Use existing patterns
2. **Always analyze first** - No guessing
3. **Only modify minimal files** - Small changes
4. **Always verify** - Run tests
5. **Always declare mode** - [PLANNER] or [EXECUTOR]

---

## Commands

```bash
# Build/Run: <!-- Add commands -->
# Test: <!-- Add commands -->
# Lint: <!-- Add commands -->
```

---

## Forbidden Actions

- DO NOT create new patterns
- DO NOT add dependencies without approval
- DO NOT skip Code Research
- DO NOT modify files outside plan
- DO NOT rewrite existing modules
- DO NOT EXECUTOR without approved plan
