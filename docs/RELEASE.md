# Release Workflow Guide

This repository publishes releases from `.github/workflows/release.yml` using `semantic-release`.

## Trigger

The workflow runs on pushes to `main`.

## Required Secret

`release.yml` uses a repository secret named:

- `SEVENTH_LAB_BOT_TOKEN`

It is used for:

- checkout with push-capable auth
- creating GitHub releases
- writing changelog/tag updates produced by semantic-release

## Token Permissions

Use a token with repository write access at minimum:

- Contents: Read and write
- Issues: Read and write
- Pull requests: Read and write

If using fine-grained PATs, scope it to this repository and grant only required permissions.

## Repository Setup Steps

1. Create a token for your bot/service account.
2. Add it as a repository secret named `SEVENTH_LAB_BOT_TOKEN`.
3. Ensure branch protections allow release automation on `main`.
4. Merge a commit with a releasable Conventional Commit type (`feat`, `fix`, etc.).

## Release Decision Rules

Configured in `.releaserc.json`:

- `feat` -> minor release
- `fix`, `perf`, `docs`, `chore`, `refactor`, `revert` -> patch release
- `test`, `build`, `ci` -> no release
- breaking changes -> major release

## Troubleshooting

### `ENOGHTOKEN` or auth errors

- Confirm `SEVENTH_LAB_BOT_TOKEN` exists
- Confirm token has required permissions
- Confirm token is not expired/revoked

### No release created

- Verify commits since last tag include releasable types
- Confirm workflow executed on `main`
- Check semantic-release logs in the `Run semantic-release` step

### Checkout/Push permission failures

- Verify bot account has write access to the repository
- Verify branch protection rules allow required automation operations

## Security Notes

- Never commit tokens to the repository
- Prefer short-lived tokens when possible
- Rotate long-lived tokens regularly
- Restrict token access to this repository when possible
