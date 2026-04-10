# Setup Guide

Use this guide to prepare a local development environment for `seventhlab/github-workflows`.

## Prerequisites

- Git
- Python 3.8+
- Node.js 20+
- pnpm
- make

## Recommended Setup

```bash
make setup
```

This command:

- installs `pre-commit`
- installs Node dependencies with `pnpm install`
- installs git hooks

## Manual Setup

```bash
make install
make install-hooks
make lint
```

## Common Commands

- `make help` - list targets
- `make lint` - run all checks
- `make lint-fix` - run checks with auto-fix
- `make update-hooks` - update pre-commit hook versions
- `make clean` - remove local caches and dependencies

## What Gets Checked

Pre-commit currently runs checks for:

- YAML validity and linting
- shell script linting (`shellcheck`)
- markdown linting (`markdownlint`)
- whitespace, merge conflict, and line ending hygiene

## First Contribution Flow

```bash
# 1) Create a branch
git checkout -b docs/update-workflow-docs

# 2) Make your changes
# ...

# 3) Run checks
make lint

# 4) Commit
git commit -m "docs: update setup and labels documentation"

# 5) Push
git push origin docs/update-workflow-docs
```

## Troubleshooting

### `pre-commit` command not found

Install dependencies first:

```bash
make install
```

### Hook fails after auto-fixes

Some hooks modify files automatically. Re-stage and run again:

```bash
git add .
make lint
```

## Related Docs

- [CONTRIBUTING.md](../CONTRIBUTING.md)
- [QUICKREF.md](./QUICKREF.md)
