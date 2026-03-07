# Testing Guide

> This document describes the testing approach for this project.

## Testing Requirements

- **Minimum Coverage**: 80%
- **Test Types**: Unit, Integration, E2E (critical flows)

## Test-Driven Development

### Workflow

```
1. RED    → Write failing test
2. GREEN  → Write minimal code to pass
3. IMPROVE → Refactor while keeping tests green
4. VERIFY → Check coverage (80%+)
```

### Example

```python
# Step 1: Write test first
def test_calculate_total_with_discount():
    items = [Item(price=100), Item(price=50)]
    result = calculate_total(items, discount=0.1)
    assert result == 135.0  # (100 + 50) * 0.9

# Step 2: Implement to pass
def calculate_total(items: list[Item], discount: float = 0) -> float:
    total = sum(item.price for item in items)
    return total * (1 - discount)
```

## Test Organization

```
tests/
├── unit/           # Fast, isolated tests
│   ├── test_utils.py
│   └── test_core.py
├── integration/    # Component interaction tests
│   └── test_api.py
└── e2e/            # End-to-end flows
    └── test_user_flow.py
```

## Test Naming

```python
# Pattern: test_<function>_<scenario>_<expected_result>
def test_process_payment_valid_card_returns_success():
    ...

def test_process_payment_expired_card_raises_error():
    ...
```

## Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src --cov-report=term-missing

# Run specific test file
pytest tests/unit/test_core.py

# Run specific test
pytest tests/unit/test_core.py::test_function_name
```

## Mocking

```python
from unittest.mock import Mock, patch

def test_external_api_call():
    with patch('module.api_client') as mock_client:
        mock_client.return_value = {"status": "ok"}
        result = process_api_call()
        assert result.success is True
```

## Reference Test Files

For test patterns, see:
- `tests/unit/test_example.py` - Unit test patterns
- `tests/integration/test_example.py` - Integration patterns
