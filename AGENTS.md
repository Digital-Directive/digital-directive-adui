# Digital Directive Agent Rules

## Branch and deployment policy

- `main` is production-facing and must not receive direct feature or fix work after the final direct-main publication on 2026-07-08.
- All future changes must land in `hml` first. Use feature branches or local work, open/merge into `hml`, validate HML, then promote `hml` to `main` by pull request.
- Pull requests into `main` must have `hml` as the source branch. Do not open feature branches directly against `main`.
- A push to `hml` is the deployment handoff for homologation. The GitHub Actions workflow `.github/workflows/hml-deploy-webhook.yml` must call the deploy webhook configured in repository secrets.
- Production deploys must happen only after HML validation and promotion from `hml` to `main`. Do not create or mutate production resources directly from local commands unless the user explicitly declares an emergency exception.
- Backend services deploy to AWS. AWS mutations must go through the approved deployment workflow/server or documented AWS deployment runbook, never by ad hoc production changes hidden from GitHub.

## Required GitHub controls

- Protect `main`: require pull requests, disallow force pushes and deletions, and require the main gate workflow.
- Keep `hml` available as the pre-production integration branch.
- Configure these repository secrets before relying on HML deploy automation:
  - `HML_DEPLOY_WEBHOOK_URL`: HTTPS endpoint on the deployment server.
  - `HML_DEPLOY_WEBHOOK_SECRET`: shared secret used to sign the webhook payload.

## Agent behavior

- Before changing production-facing code, check the current branch and remote state.
- Prefer committing to `hml` or a feature branch. Do not create new direct commits on `main`.
- Keep secrets out of Git. Use credential vaults or GitHub secrets.
- When deployment behavior changes, update this file and the relevant workflow in the same PR.
