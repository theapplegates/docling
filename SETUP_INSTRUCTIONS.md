# Docling — Local Setup Instructions

Steps used to set up this clone of [theapplegates/docling](https://github.com/theapplegates/docling.git) on macOS (verified 2026-09-23, Docling 2.130.0).

## Prerequisites

- **uv** — `brew install uv` (verified with uv 0.12.18)
- **Python 3.10+** — uv will fetch a suitable interpreter automatically
- **git**

## 1. Clone (if starting fresh)

```bash
git clone https://github.com/theapplegates/docling.git
cd docling
```

## 2. Ensure the working tree is complete

This clone initially had the entire `docling/` package directory missing from
disk (278 files showed as deleted in `git status`). Check and, if needed,
restore:

```bash
git status --short        # should print nothing
git checkout -- docling/  # restore package files if they show as deleted
```

## 3. Install the development environment

```bash
make setup
```

This runs:

```bash
uv sync --frozen --group dev --all-extras --no-group docs --no-group examples
```

It creates a `.venv/` and installs the package in editable mode with all
extras and dev dependencies.

## 4. Verify the install

```bash
uv run docling --version
uv run python -c "import docling; print(docling.__version__)"
```

Expected output includes `Docling version: 2.130.0` and a working import.

## Day-to-day commands

```bash
make test        # run the pytest suite
make check       # read-only local checks
make validate    # mutating hooks (formatting/linting) on current changes
uv run docling <file.pdf>   # convert a document with the CLI
```

## Optional

```bash
make hooks-install   # install git hooks via prek
```
