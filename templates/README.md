# CLAUDE.md Templates

Ready-to-use templates for configuring Claude Code AI behavior.

---

## Quick Start

```bash
# For general projects
cp templates/CLAUDE.md /your/project/CLAUDE.md

# For quantitative trading projects
cp templates/CLAUDE_QUANT.md /your/project/CLAUDE.md
```

Then customize the Project Overview and Commands sections.

---

## Templates

### CLAUDE.md
**Use for**: General software projects
**Features**:
- 7-phase development workflow
- Code Research requirement
- Progressive disclosure via agent_docs
- Minimal, focused rules

### CLAUDE_QUANT.md
**Use for**: Quantitative trading / strategy development
**Features**:
- Controller/Executor architecture reference
- pandas_ta integration
- Backtest workflow
- Strategy development phases

---

## Agent Documentation Templates

### architecture.md
Documents system architecture with:
- Component descriptions
- Data flow diagrams
- Key file references
- Pattern examples

### code_conventions.md
Defines coding standards:
- Naming conventions
- File organization
- Error handling patterns
- Type hint requirements

### testing_guide.md
Testing approach and standards:
- TDD workflow
- Test organization
- Coverage requirements (80%)
- Running tests

### debugging.md
Systematic debugging procedures:
- Bug reproduction
- Isolation techniques
- Fix guidelines
- Verification checklist

---

## Agent Architecture Templates

### master_control.md
The orchestration agent that:
- Decomposes goals into tasks
- Controls execution loops
- Coordinates other agents
- Tracks progress

### analysis_agent.md
The analysis agent that:
- Examines code and data
- Generates hypotheses
- Identifies gaps
- Recommends next steps

### executor_agent.md
The execution agent that:
- Runs minimal experiments
- Validates hypotheses
- Collects metrics
- Reports standardized results

### strategy_lab.md
The knowledge system that:
- Records all experiments
- Persists learnings
- Builds pattern library
- Enables querying history

---

## Design Principles

1. **Less is More** - CLAUDE.md should be < 100 lines
2. **Progressive Disclosure** - Details in agent_docs, not main file
3. **Executable Rules** - AI knows exactly what to do
4. **Strong Constraints** - Prevents bad code patterns
5. **Closed Loops** - Problem → Solution → Code → Verify → Back

---

## Directory Structure

```
templates/
├── CLAUDE.md              # General project template
├── CLAUDE_QUANT.md        # Quantitative trading template
├── QUICKSTART.md          # Quick start guide
│
└── agent_docs/
    ├── architecture.md
    ├── code_conventions.md
    ├── testing_guide.md
    ├── debugging.md
    │
    ├── master_control.md
    ├── analysis_agent.md
    ├── executor_agent.md
    └── strategy_lab.md
```

---

## Related Documentation

- `docs/RESEARCH_REPORT.md` - Comprehensive research findings
- `docs/DISCUSSION_SUMMARY.md` - Design rationale and discussion
