# GitHub Labels and Auto-Labeling

This repository uses [actions/labeler](https://github.com/actions/labeler) to automatically apply labels to pull requests.

## Configuration Source

Auto-labeling rules are defined in:

- `.github/labeler.yml`

The workflow that applies those rules is:

- `.github/workflows/pr-labeling.yml`

## Labels Used

Create these labels in GitHub (or adjust names in `.github/labeler.yml`):

| Label | Suggested Color | Description |
| --- | --- | --- |
| `feature` | `a2eeef` | Feature work (`feat/*` branches) |
| `bug` | `d73a4a` | Bug fixes (`fix/*`, `bugfix/*`, `hotfix/*`) |
| `documentation` | `0075ca` | Markdown and docs changes |
| `ci/cd` | `d4c5f9` | CI/workflow automation updates |
| `maintenance` | `fbca04` | Repository maintenance/config cleanup |
| `dependencies` | `0366d6` | Dependency and lockfile updates |
| `testing` | `0e8a16` | Test workflow/test artifact updates |
| `performance` | `ff6b6b` | Performance-focused changes (`perf/*`) |
| `refactor` | `5319e7` | Refactoring work (`refactor/*`) |
| `breaking-change` | `b60205` | Breaking API/interface changes |

## Rule Summary

### By Branch Name

- `feature`: `^feat/` or `^feature/`
- `bug`: `^fix/`, `^bugfix/`, `^hotfix/`
- `documentation`: `^docs/`
- `ci/cd`: `^ci/`
- `maintenance`: `^chore/`
- `dependencies`: `^deps/`, `^dependabot/`, `^renovate/`
- `testing`: `^test/`
- `performance`: `^perf/`
- `refactor`: `^refactor/`
- `breaking-change`: branch name ending with `!`

### By Changed Files

- `documentation`: `**/*.md`, `docs/**/*`
- `ci/cd`:
  - `.github/workflows/**/*`
  - `.github/labeler.yml`
- `maintenance`:
  - `.gitignore`
  - `.markdownlint.json`
  - `.pre-commit-config.yaml`
  - `.releaserc.json`
  - `Makefile`
  - `LICENSE`
- `dependencies`: `package.json`, `pnpm-lock.yaml`, `.pre-commit-config.yaml`
- `testing`: `.github/workflows/tests.yml`, `**/*test*`, `**/*spec*`, `coverage/**/*`

### By PR Body Content

- `breaking-change`: PR body includes `BREAKING CHANGE` or `BREAKING-CHANGE`

## Quick Setup with GitHub CLI

```bash
gh label create "feature" --color "a2eeef" --description "Feature work"
gh label create "bug" --color "d73a4a" --description "Bug fix"
gh label create "documentation" --color "0075ca" --description "Documentation changes"
gh label create "ci/cd" --color "d4c5f9" --description "CI/CD and workflow changes"
gh label create "maintenance" --color "fbca04" --description "Maintenance and config updates"
gh label create "dependencies" --color "0366d6" --description "Dependency updates"
gh label create "testing" --color "0e8a16" --description "Testing related changes"
gh label create "performance" --color "ff6b6b" --description "Performance improvements"
gh label create "refactor" --color "5319e7" --description "Refactor work"
gh label create "breaking-change" --color "b60205" --description "Breaking changes"
```

## Testing Labeler Changes

1. Update `.github/labeler.yml`.
2. Open a PR from a branch that matches one of the branch rules.
3. Change files that match one or more path filters.
4. Confirm labels were applied by the `PR Labeling` workflow.

## Customization

Adjust `.github/labeler.yml` to fit your repository conventions. Keep this document in sync when rules or labels change.
