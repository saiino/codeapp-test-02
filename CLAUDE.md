# Repository conventions

This repository was scaffolded by [claude-code-repo-template](https://github.com/saiino/claude-code-repo-template).

## Branching

- `main`: aggregates completed feature work. Protected 窶・no direct push, PR required.
- `release/dev`: deploys to the Power Platform Development environment on merge.
- `release/prod`: deploys to the Power Platform Production environment on merge.
- `feature/*`: working branches for individual features/fixes.

## Workflow

1. Branch from `main` as `feature/<name>`.
2. Open a PR into `main` and merge.
3. Open a PR from `main` into `release/dev`. Merging triggers `.github/workflows/deploy.yml`, deploying to the Development Power Platform environment.
4. After verifying in Dev, open a PR from `release/dev` (or `main`) into `release/prod`. Merging deploys to Production.

## Branch protection

`main`, `release/dev`, and `release/prod` all require a pull request and block direct pushes, including for admins (`enforce_admins: true`). Required approving review count is 0: this is a single-maintainer setup, GitHub does not allow self-approval, and raising this above 0 would make merges impossible without a second collaborator. Raise it once there are multiple maintainers.

## Secrets

Power Platform credentials live in GitHub Environments `Development` / `Production` as `PAC_TENANT_ID`, `PAC_CLIENT_ID`, `PAC_CLIENT_SECRET`, `PAC_ENV_URL`. Replace the placeholder (`REPLACE_ME`) values before relying on real deploys.
