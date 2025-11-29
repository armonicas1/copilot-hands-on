# Copilot Agent Instructions

## Project Overview
This is a **Python Flask web application** used for GitHub Copilot hands-on training. The codebase demonstrates authentication patterns, data storage abstractions, and utility functions.

## Tech Stack & Defaults
- **Python:** 3.10+
- **Framework:** Flask ≥2.0.0
- **Testing:** pytest ≥7.0.0
- **Package Management:** pip with `requirements.txt`
- **Dev Environment:** VS Code devcontainer

## Repository Structure
```
├── app/                 # Flask application
│   ├── app.py          # Main Flask app entry point
│   ├── auth.py         # Authentication module
│   └── datastore.py    # Data storage abstraction
├── scripts/            # Utility scripts
├── extra/              # Supplementary materials
├── prime.py            # Standalone utility (prime number checker)
├── requirements.txt    # Python dependencies
└── .devcontainer/      # Devcontainer configuration
```

## Code Style & Conventions

### Python
- Use **type hints** on all function signatures
- Follow **Google-style docstrings** with `Args`, `Returns`, and `Example` sections
- Keep functions focused and under 50 lines where possible
- Use `snake_case` for functions/variables, `PascalCase` for classes

### Do
```python
def calculate_total(items: list[dict], tax_rate: float = 0.1) -> float:
    """Calculate total price including tax.

    Args:
        items: List of item dictionaries with 'price' key.
        tax_rate: Tax rate as decimal. Defaults to 0.1.

    Returns:
        Total price including tax.

    Example:
        >>> calculate_total([{"price": 10}, {"price": 20}], 0.1)
        33.0
    """
    subtotal = sum(item["price"] for item in items)
    return subtotal * (1 + tax_rate)
```

### Don't
```python
def calc(i, t=0.1):  # No type hints, unclear names, no docstring
    return sum(x["price"] for x in i) * (1 + t)
```

## Testing Requirements
- Run tests with: **`pytest`**
- Place tests in files named `test_*.py` or `*_test.py`
- Cover both success and failure paths
- Add regression tests when fixing bugs

## Flask Application Guidelines
- Entry point: `app/app.py`
- Keep routes thin; delegate logic to service modules
- Use `app/auth.py` patterns for authentication
- Use `app/datastore.py` patterns for data access

## Development Workflow

### Local Setup
```bash
pip install -r requirements.txt
```

### Running the App
```bash
cd app && python app.py
```

### Running Tests
```bash
pytest
```

## Git & PR Conventions
- **Branch naming:** `feature/*`, `fix/*`, `chore/*`
- **Commits:** Conventional Commits format (e.g., `feat(auth): add token validation`)
- **PR size:** Target ≤300 lines of code for reviewability
- **Checklist:** Ensure tests pass, no linting errors, docstrings updated

## Security & Secrets
- **Never** commit secrets, API keys, or credentials
- Use environment variables for sensitive configuration
- Document required env vars in `.env.example` if applicable

## Agent Behavior
1. **Before modifying code:** Understand existing patterns in `app/` directory
2. **When adding features:** Follow the module structure (separate concerns)
3. **When fixing bugs:** Add a regression test
4. **When uncertain:** Check existing implementations in `auth.py` or `datastore.py` for patterns
5. **Dependencies:** Justify additions; update `requirements.txt`; ensure compatibility with Python 3.10+
