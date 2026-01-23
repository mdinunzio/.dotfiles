# Project Preferences

## Python Standards

- Use Python 3.11+ features where beneficial
- Type hints required on all function signatures
- Google-style docstrings for all public functions and classes
- PEP 8 compliance enforced via flake8
- Format with black (line length 88)
- Sort imports with isort (black-compatible profile)
- Use `uv` as the package manager (not pip or poetry)
- Use `click` for CLI argument parsing
- Use `python-dotenv` for environment variable loading
- Use `pytest` for all testing (unit and integration)

## Code Style

- Prefer functions over classes for data manipulation
- Use classes only when: managing state, polymorphism is needed, or using dataclasses/Pydantic models
- Keep functions under 50 lines; refactor if longer
- Keep files under 400 lines; split if larger
- Limit function parameters to 5-7; use dataclasses or config objects for more
- Use early returns to reduce nesting
- Name variables descriptively: `user_count` not `n`, `is_valid` not `flag`

## Error Handling

- Use specific exception types, not bare `except:`
- Create custom exceptions in a dedicated `exceptions.py` when domain-specific errors are needed
- Log errors with context before re-raising
- Fail fast: validate inputs at function boundaries

## Naming Conventions for Functions

### Functions that Read Data
- When reading data from an external source with a potentially expensive delay (e.g. HTTP request or database select) use the `fetch_` prefix for the function name (e.g. `fetch_customer_transactions`)
- When reading data from the disk or a network drive use the `load_` prefix for the function name (e.g. `load_training_parquet`)
- When reading data from memory or creating an inexpensive data structure in-memory sources use the `get_` prefix for the function name (e.g. `get_customer_dataframe` or `get_id_to_name_mapping`)

## Other Functions
- Other functions should generally be a verb that describes what its role is (e.g. `refine_customer_transactions` or `encode_url`)
- Exceptions can be made to the above rule for boolean queries (e.g. `is_valid`)

## Project Structure
```
project_name/
├── project_name/          # Source (same name as project, not src/)
│   ├── __init__.py        # Contains __version__
│   ├── settings.py        # Constants, logging config, env loading
│   ├── exceptions.py      # Custom exceptions
│   └── ...
├── tests/
│   ├── conftest.py
│   ├── test_*.py
│   └── ...
├── main.py                # Entry point for applications
├── .env                   # Secrets (never committed)
├── .env.example           # Template with dummy values
├── .gitignore
├── pyproject.toml
├── CHANGELOG.md
└── README.md
```

- Import `settings.py` first in `__init__.py` to initialize logging and constants
- Use semantic versioning (MAJOR.MINOR.PATCH)
- Store version string in `__init__.py` as `__version__`
- main.py should neighbor the project_name (src/ equivalent) folder, so it can  import all modules without sys.path modification

## Testing (TDD)

1. Write failing tests first that define expected behavior
2. Implement minimum code to pass tests
3. Refactor while keeping tests green
4. Aim for >80% coverage on business logic

## Security

- NEVER hardcode secrets, API keys, or credentials
- All sensitive values go in `.env` (add to `.gitignore`)
- Use `.env.example` with placeholder values for documentation
- Before committing, verify no secrets in diff

## Git Conventions

- Commit messages: `type: short description` (e.g., `feat: add user authentication`)
- Types: feat, fix, docs, style, refactor, test, chore
- Keep commits atomic (one logical change per commit)

## Changelog

- Follow https://keepachangelog.com format
- Categories: Added, Changed, Deprecated, Removed, Fixed, Security
- Update changelog with each meaningful change

## Claude Code Behavior

- When modifying existing code, match the existing style even if it differs from these preferences
- Ask before making architectural changes that affect multiple files
- Run tests after changes and fix any failures before considering work complete
- If a task is ambiguous, ask for clarification rather than guessing
- When adding dependencies, check if an existing dependency already solves the problem