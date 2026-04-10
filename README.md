# GitHub Workflows Collection

A curated collection of GitHub workflows for CI/CD, testing, linting, release automation, and pull request hygiene.

This repository also centralizes pinned baseline actions (checkout/setup-node/setup-go) through `seventhlab/github-actions`
so workflow consumers can use consistent tooling across repositories.

## Reusable Workflows (For Other Repositories)

Only workflows with a `workflow_call` trigger are reusable from other repositories.

| Workflow | File | Trigger | Purpose |
| --- | --- | --- | --- |
| Pre-commit checks | `.github/workflows/pre-commit.yml` | `workflow_call` | Reusable lint/format gate with optional Node and Go setup |
| Service tests | `.github/workflows/tests.yml` | `workflow_call` | Reusable CDK and Go test pipeline with Sonar scan |

## Repository-Internal Workflows

These workflows are for this repository's own automation and are not designed to be consumed via `uses: ...`.

| Workflow | File | Trigger | Purpose |
| --- | --- | --- | --- |
| Repo lint | `.github/workflows/lint.yml` | `push`, `pull_request` | Runs pre-commit checks for this repository |
| PR labeling | `.github/workflows/pr-labeling.yml` | `pull_request` | Auto-applies labels based on file paths and branch names |
| Release | `.github/workflows/release.yml` | `push` to `main` | Runs semantic-release and publishes releases |

## Reusing Workflows

Reference reusable workflows from this repository using:

```yaml
jobs:
  lint:
    uses: seventhlab/github-workflows/.github/workflows/pre-commit.yml@v1
```

Use tags for stable consumption:

- `@v1.2.3` for fully pinned releases
- `@v1` for major-only updates
- `@main` for development/testing only

Reusable workflows in this repository are currently:

- `.github/workflows/pre-commit.yml`
- `.github/workflows/tests.yml`

### Example with Inputs and Secrets

```yaml
jobs:
  tests:
    uses: seventhlab/github-workflows/.github/workflows/tests.yml@v1
    with:
      node-version: 24
      go-version: '1.26.1'
      run-cdk-tests: true
      run-go-tests: true
    secrets:
      NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

## Local Development

### Prerequisites

- Python 3.8+ (for `pre-commit`)
- Node.js 20+
- `pnpm`
- `make`

### Setup

```bash
git clone https://github.com/seventhlab/github-workflows.git
cd github-workflows
make setup
```

### Common Commands

- `make help` - list available commands
- `make lint` - run all pre-commit checks
- `make lint-fix` - run checks with auto-fix where supported
- `make test` - alias to lint checks for this repository
- `make clean` - remove local caches and generated artifacts

## Contributing

Contribution details are in [CONTRIBUTING.md](./CONTRIBUTING.md).

Additional docs:

- [docs/SETUP.md](./docs/SETUP.md)
- [docs/QUICKREF.md](./docs/QUICKREF.md)
- [docs/LABELS.md](./docs/LABELS.md)
- [docs/RELEASE.md](./docs/RELEASE.md)
- [docs/SECURITY.md](./docs/SECURITY.md)

## Commit and Release Conventions

This repo uses Conventional Commits and semantic-release.

- `feat`, `fix`, `perf`, `docs`, `chore`, `refactor` can trigger releases
- `test`, `build`, `ci` do not trigger releases by default
- breaking changes trigger major releases

Release configuration lives in `.releaserc.json`.

## License

MIT License - see [LICENSE](./LICENSE).

## Support

- Issues: <https://github.com/seventhlab/github-workflows/issues>
- Security: [docs/SECURITY.md](./docs/SECURITY.md)
