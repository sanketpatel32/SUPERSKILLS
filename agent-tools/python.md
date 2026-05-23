# Python

Use this rule automatically when the repo is a Python project.

## Detect Python Repos

Treat the workspace as Python when you see any of:
- `pyproject.toml`
- `uv.lock`
- `requirements.txt`
- `setup.py`
- `setup.cfg`
- `poetry.lock`
- `.python-version`
- Python packages or modules with `.py` files

If `uv.lock` or `pyproject.toml` exists, assume `uv` is the preferred workflow unless the repo clearly documents otherwise.

In multi-repo workspaces, inspect the nearest service directory first. Do not assume the workspace root is the runnable project.

## Default Command Style

Prefer project scripts through `uv`:

```powershell
uv run dev
uv run prod
uv run lint
uv run test
```

If `pyproject.toml` has `[project.scripts]`, use those script names exactly:

```powershell
uv run dev
uv run prod
uv run lint
uv run format
uv run lint-fix
uv run typecheck
uv run test
uv run check
```

If those scripts do not exist, inspect `pyproject.toml`, `README.md`, or task runner config before guessing.

Do not switch to raw `python`, `pip`, `pytest`, `ruff`, or `mypy` commands unless:
- the repo documents that command
- `uv run ...` is unavailable
- the user specifically asks for it

## Before Editing

Check the project shape first:
- package manager and Python version
- available scripts/tasks
- test framework
- lint/format tools
- app entrypoints
- whether broad tests are known to fail for unrelated reasons

Prefer reading:
- `pyproject.toml`
- `README.md`
- `.python-version`
- `uv.lock` only when dependency details matter

Do not run `uv sync` or install dependencies unless needed to run/verify the requested task.

## Verification

For code changes, verify with the smallest relevant command first:
- targeted test for bug fixes
- `uv run lint` for lint-sensitive edits
- `uv run typecheck` when typing or interfaces changed
- `uv run test` when behavior may be affected broadly

If a command fails because the script does not exist, report that clearly and fall back to the closest documented command.
If broad tests fail during collection or for unrelated existing issues, report the exact blocker and run focused tests for the touched area.
When changing app entrypoints or config, prefer a startup/import check before broad tests.

## Dependency Rules

- Do not add dependencies unless necessary.
- Prefer `uv add <package>` for runtime dependencies.
- Prefer `uv add --dev <package>` for development dependencies.
- Do not edit lockfiles manually.
- After dependency changes, run the relevant verification command.

## Runtime Rules

When the user asks to run the app, prefer:

```powershell
uv run dev
```

For production-like runs, prefer:

```powershell
uv run prod
```

If the app uses FastAPI, Flask, Django, Celery, or another framework, still prefer the repo's `uv` script first. Only use framework-specific commands after confirming the repo expects them.

If `.python-version` or `requires-python` pins a version, respect it when syncing or running. Example:

```powershell
uv sync --python 3.13
uv run --python 3.13 dev
```

## Style Rules

- Keep changes small and idiomatic.
- Preserve existing typing style.
- Avoid broad refactors while fixing bugs.
- Prefer explicit, boring code over clever abstractions.
- Do not introduce global state or import-time side effects unless the repo already uses that pattern.
