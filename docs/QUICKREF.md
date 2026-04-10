# Quick Reference

## Setup

```bash
make setup
make install
make install-hooks
```

## Quality Checks

```bash
make lint
make lint-fix
make test
```

## Maintenance

```bash
make update-hooks
make clean
make help
```

## Workflow Scope

Only workflows with a `workflow_call` trigger are reusable from other repositories.

Reusable workflows:

- `.github/workflows/pre-commit.yml`
- `.github/workflows/tests.yml`

Repository-internal workflows:

- `.github/workflows/lint.yml`
- `.github/workflows/pr-labeling.yml`
- `.github/workflows/release.yml`

## Conventional Commit Format

```text
<type>[optional scope]: <description>
```

### Common Types

- `feat` - new capability
- `fix` - bug fix
- `docs` - documentation changes
- `chore` - maintenance tasks
- `refactor` - refactor without behavior change
- `test` - tests only
- `ci` - CI/CD config changes
- `perf` - performance improvements
- `build` - build or dependency tooling

### Breaking Change

```text
feat!: change workflow interface
```

or include:

```text
BREAKING CHANGE: describe migration steps
```

## Branch Naming

```text
feat/<name>
fix/<name>
docs/<name>
chore/<name>
refactor/<name>
test/<name>
ci/<name>
perf/<name>
```

## Typical Workflow

```bash
# 1) setup
make setup

# 2) branch
git checkout -b feat/add-reusable-workflow

# 3) edit files
# ...

# 4) verify
make lint

# 5) commit
git commit -m "feat: add reusable lint workflow inputs"

# 6) push
git push origin feat/add-reusable-workflow
```

## Key Files

| File | Purpose |
| --- | --- |
| `Makefile` | Local contributor commands |
| `.pre-commit-config.yaml` | Lint/check hook definitions |
| `.releaserc.json` | Semantic-release behavior |
| `.github/workflows/` | Reusable and repo workflows |
| `.github/labeler.yml` | PR auto-labeling filters |
| `docs/` | Contributor and ops documentation |
