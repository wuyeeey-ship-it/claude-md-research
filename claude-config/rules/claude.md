# AI Development Workflow

> This file defines the mandatory development workflow that applies to all projects.

## Critical Rules

1. **Never invent code structures** - Use existing patterns only
2. **Always analyze existing code first** - No guessing
3. **Only modify minimal necessary files** - Small changes
4. **Every solution must be verified** - Run tests always
5. **Never modify additional files during implementation** - If new files are required, return to planning phase and update the plan
6. **Always reuse existing implementations** - Extend or reuse existing code whenever possible. Do NOT reimplement functionality that already exists

---

## Development Workflow (MANDATORY)

Follow these phases in order. **Never skip phases.**

### PHASE 1: Requirement Analysis
- Understand the problem completely
- Define success criteria
- Identify constraints
- **Output**: Clear problem statement

### PHASE 2: Code Research
(must include file + line reference)
- **STOP**: Do not write code yet
- Search for existing implementations
- Document findings with exact references:
  ```
  ## Research Findings
  - File: path/to/file.py
    Lines: 35-110
    Class/Function: ClassName
    Purpose: What it does
  ```
- **Output**: Research notes with exact references

### PHASE 3: Solution Planning
(must list files to modify)
- Design solution based on research
- List exact files to modify:
  ```
  ## Files to Modify
  1. path/to/file1.py (lines 50-80) - Description
  2. path/to/file2.py (new function) - Description

  ## Implementation Plan
  Step 1: ...
  Step 2: ...
  ```
- **Output**: Plan with exact file list

### PHASE 4: Implementation
(minimal modification only)
- Write code following plan
- Follow existing patterns exactly
- **DO NOT rewrite existing modules**
- Only extend or minimally modify
- Only modify files listed in PHASE 3
- **Output**: Working code

### PHASE 5: Verification
- Run tests
- Check types/linting
- Verify functionality
- **Output**: Test results

### PHASE 6: Requirement Validation
- Compare against original requirements
- Check completeness
- **Output**: Validation report

### PHASE 7: Iteration Loop
- If issues found → Return to PHASE 1
- If complete → Commit changes

---

## Forbidden Actions

- DO NOT create new architectural patterns
- DO NOT add dependencies without approval
- DO NOT skip the Code Research phase
- DO NOT modify files outside minimal scope
- DO NOT rewrite existing modules (extend only)
