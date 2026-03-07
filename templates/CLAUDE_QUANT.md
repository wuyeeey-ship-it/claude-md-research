# Quantitative Development AI Rules

> **CRITICAL**: Never write code before completing the Code Research step.

---

## Project Overview

**Purpose**: Quantitative trading strategy development and backtesting

**Tech Stack**:
- Python 3.x
- pandas_ta (technical indicators)
- Hummingbot framework
- Controller/Executor architecture

---

## Development Workflow (MANDATORY)

### PHASE 1: Requirement Analysis
- Define the trading problem
- Identify market conditions
- Set success metrics (win rate, Sharpe, etc.)
- **Output**: Strategy requirements document

### PHASE 2: Code Research
- **STOP**: Do not write code yet
- Study existing strategies in `strategies/`
- Review Controller/Executor patterns
- Check pandas_ta indicator docs
- **Output**: Research notes with file:line references

### PHASE 3: Strategy Design
- Define entry/exit signals
- Design risk management rules
- Plan position sizing
- **Output**: Strategy specification

### PHASE 4: Implementation
- Create Executor with signal logic
- Wire into Controller framework
- Follow existing patterns exactly
- **Output**: Working strategy code

### PHASE 5: Backtesting
- Run historical simulation
- Analyze metrics
- Identify edge cases
- **Output**: Backtest results

### PHASE 6: Validation
- Compare against requirements
- Check risk parameters
- Verify edge case handling
- **Output**: Validation report

### PHASE 7: Iteration Loop
- If issues → Return to PHASE 1
- If ready → Paper trading

---

## Critical Rules

1. **Never invent code structures** - Follow Controller/Executor pattern
2. **Always use pandas_ta** - No custom indicator math
3. **Always reference existing strategies** - No guessing
4. **Only modify minimal necessary files**

---

## Architecture Reference

### Controller/Executor Pattern

```
Controller
├── Orchestrates strategy lifecycle
├── Manages data feeds (candles)
└── Calls Executor methods

Executor
├── Implements signal logic
├── Returns standardized signals
└── No direct trading operations
```

**Reference Files**:
- `controllers/example_controller.py:10-100` - Controller pattern
- `executors/example_executor.py:10-80` - Executor pattern

### Data Structures

```python
# Candle data structure (candles feed)
candles = {
    "timestamp": [...],
    "open": [...],
    "high": [...],
    "low": [...],
    "close": [...],
    "volume": [...]
}

# Signal output format
signal = {
    "action": "LONG" | "SHORT" | "NEUTRAL",
    "confidence": 0.0 - 1.0,
    "metadata": {...}
}
```

---

## Agent Documentation

Read before complex tasks:

- `agent_docs/hummingbot_integration.md` - Hummingbot setup
- `agent_docs/indicator_library.md` - pandas_ta usage
- `agent_docs/backtest_workflow.md` - Testing strategies
- `agent_docs/risk_management.md` - Risk parameters

---

## Forbidden Actions

- DO NOT create new architectural patterns
- DO NOT write custom indicator calculations (use pandas_ta)
- DO NOT bypass the Controller/Executor separation
- DO NOT skip backtesting before paper trading

---

## Quick Reference

```bash
# Run backtest
python scripts/backtest.py --strategy <name>

# Check types
mypy strategies/

# Run tests
pytest tests/strategies/
```
