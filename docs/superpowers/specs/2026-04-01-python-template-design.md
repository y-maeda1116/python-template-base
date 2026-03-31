# Python Template Base - Design Spec

## Overview

Minimal Python template for CLI/script projects with security integration via [security-base](https://github.com/y-maeda1116/security-base).

## Requirements

- Python 3.13
- Package management: `pyproject.toml` (PEP 621)
- Tools: Ruff (lint/format), mypy (type check), pytest (test)
- CI: GitHub Actions (lint, type check, test, security)
- Security: Referenced from `y-maeda1116/security-base`

## Project Structure

```
python-template-base-/
├── .github/
│   ├── workflows/
│   │   ├── ci.yml              # Ruff + mypy + pytest on PR/push
│   │   ├── python-security.yml # calls security-base reusable-py-security.yml
│   │   └── secret-scan.yml     # calls security-base reusable-secret-scan.yml
│   └── dependabot.yml          # weekly GitHub Actions updates
├── src/
│   └── __init__.py
├── tests/
│   └── __init__.py
├── pyproject.toml
└── README.md
```

## Tooling

### uv (package manager + runner)
- All CI commands run via `uv run`
- Dependencies managed through `[dependency-groups] dev` in pyproject.toml

## Security Integration

All security workflows are reusable from `y-maeda1116/security-base@main`.

### python-security.yml

Calls `reusable-py-security.yml` with:
- `python-version: "3.13"`
- Runs `pip-audit --strict` and `bandit -r . -ll`

### secret-scan.yml

Calls `reusable-secret-scan.yml` with:
- `scan-tool: "trivy"`

### dependabot.yml

Weekly updates for GitHub Actions dependencies. Mirrors the security-base configuration.

## pyproject.toml Configuration

### Ruff
- `target-version = "py313"`
- `line-length = 88`
- Select rules: E, F, I, N, UP, B, A, SIM

### mypy
- `strict = true`

### pytest
- Default configuration, 80% coverage target

## CI Workflow (ci.yml)

Triggers on: pull_request, push to main

Jobs:
1. Install uv + set up Python 3.13
2. Ruff lint (`uv run ruff check .`)
3. Ruff format check (`uv run ruff format --check .`)
4. mypy (`uv run mypy src`)
5. pytest (`uv run pytest`)

## Out of Scope

- CLI framework (click/typer) - add as needed
- Docker/Makefile - add as needed
- Logging configuration - add as needed
