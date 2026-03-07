# Code Conventions

> This document defines coding standards for this project.

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables | snake_case | `user_count` |
| Functions | snake_case | `calculate_total()` |
| Classes | PascalCase | `OrderProcessor` |
| Constants | UPPER_SNAKE | `MAX_RETRY_COUNT` |
| Private | _leading_underscore | `_internal_helper()` |

## File Organization

```
module/
├── __init__.py      # Public interface
├── core.py          # Core logic
├── utils.py         # Helper functions
└── tests/
    └── test_core.py # Tests mirror structure
```

## Code Style

### Function Size
- Maximum 50 lines per function
- Single responsibility
- Extract helpers when needed

### File Size
- Maximum 400 lines per file
- High cohesion, low coupling

### Nesting
- Maximum 4 levels of nesting
- Extract to helper functions

### Documentation
- Docstrings for public APIs
- Comments for non-obvious logic only
- Let code be self-documenting

## Error Handling

```python
# Good: Explicit error handling
def process_data(data):
    if not data:
        raise ValueError("data cannot be empty")
    # process...

# Bad: Silent failure
def process_data(data):
    if not data:
        return None  # Hides problems
```

## Type Hints

```python
# Always use type hints for function signatures
def calculate_total(items: list[Item]) -> float:
    return sum(item.price for item in items)
```

## Reference Files

For actual code examples, see:
- `src/core/example.py:10-50` - Good function example
- `src/utils/helpers.py:20-40` - Utility pattern
