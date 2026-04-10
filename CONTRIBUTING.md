# Contributing to GitHub Workflows Collection

Thanks for contributing. This repository contains reusable GitHub workflows and supporting automation used across
SeventhLab repositories.

Only workflows that include a `workflow_call` trigger are reusable by other repositories. Workflows without
`workflow_call` are repository-internal automation.

## Quick Start

```bash
git clone https://github.com/<your-username>/github-workflows.git
cd github-workflows
make setup
```

Setup installs dependencies and pre-commit hooks.

## Local Commands

- `make help` - list available targets
- `make setup` - install dependencies and git hooks
- `make install` - install Python and Node dependencies
- `make install-hooks` - install pre-commit hook
- `make lint` - run all pre-commit checks
- `make lint-fix` - run checks with auto-fix
- `make clean` - remove local caches and generated files

## Branch Naming

Use descriptive prefixes:

- `feat/<name>`
- `fix/<name>`
- `docs/<name>`
- `chore/<name>`
- `refactor/<name>`
- `test/<name>`
- `ci/<name>`
- `perf/<name>`

## Development Workflow

1. Create a branch from `main`.
2. Make focused changes to workflows, docs, or config.
3. Run `make lint` locally.
4. Commit using Conventional Commits.
5. Push and open a pull request.

## Reusable Workflow Guidelines

When changing files under `.github/workflows/`:

1. Prefer `workflow_call` for reusable workflows.
2. Keep inputs typed and documented (`description`, `required`, `default`).
3. Keep secrets explicit and minimal.
4. Pin external actions to tagged versions.
5. Keep `permissions` as narrow as possible.
6. Update docs when behavior, inputs, or required secrets change.

Current reusable workflows:

- `.github/workflows/pre-commit.yml`
- `.github/workflows/tests.yml`

## Testing Changes

### Local quality gate

```bash
make lint
```

### Integration validation in a consumer repository

For reusable workflow updates, validate by calling the workflow from a test repository:

```yaml
jobs:
  lint:
    uses: seventhlab/github-workflows/.github/workflows/pre-commit.yml@main
```

Then switch to a release tag (`@v1`, `@v1.2.3`) once changes are published.

## Commit Message Rules

This repository uses [Conventional Commits](https://www.conventionalcommits.org/).

Format:

```text
<type>[optional scope]: <description>
```

Common types:

- `feat` - new capability
- `fix` - bug fix
- `docs` - documentation update
- `chore` - maintenance
- `refactor` - refactor without behavior change
- `test` - test-only changes
- `ci` - CI workflow/config changes
- `perf` - performance improvements
- `build` - build/dependency tooling

Breaking changes:

- add `!` after the type, or
- add `BREAKING CHANGE:` in the commit body/footer.

Examples:

```bash
git commit -m "feat: add reusable workflow for release previews"
git commit -m "fix: correct default go-version input in tests workflow"
git commit -m "docs: update workflow usage examples"
```

## Pull Request Checklist

Before requesting review:

- [ ] Changes are scoped and explained clearly
- [ ] `make lint` passes
- [ ] Documentation is updated when behavior changed
- [ ] Required secrets/inputs changes are documented
- [ ] Commit history follows Conventional Commits

## Release Notes Behavior

Releases are generated with semantic-release on pushes to `main`.

By default in `.releaserc.json`:

- `feat` -> minor release
- `fix`, `perf`, `docs`, `chore`, `refactor`, `revert` -> patch release
- `test`, `build`, `ci` -> no release

## Need Help?

- Issues: <https://github.com/seventhlab/github-workflows/issues>
- Security: [docs/SECURITY.md](./docs/SECURITY.md)
