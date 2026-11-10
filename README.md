# devops-2025S-demo
class demo for devops class
pretending to add more details to the readme
completed.

## Local Django secret

The application reads `DJANGO_SECRET_KEY` from the environment. For local
development, generate a fresh key with
`python -c "import secrets; print(secrets.token_hex(32))"` and put it in the
ignored `.env` file as `DJANGO_SECRET_KEY=<generated-key>`. Do not commit `.env`;
it is already listed in `.gitignore`.

## Security checks

Install the commit hooks with `pre-commit install`. Ruff linting, Ruff
formatting, and Gitleaks then run against staged changes. Pull requests also run
Bandit, Gitleaks, Trivy, and Checkov:

- Bandit reports all severity levels but is advisory and does not block the
  workflow. The original low-severity hard-coded key finding has been
  remediated; the team can tighten this gate after reviewing future reports.
- Gitleaks blocks detected secrets.
- Trivy blocks fixable CRITICAL image vulnerabilities.
- Checkov blocks Terraform findings. Any accepted finding must be recorded with
  its justification in [SECURITY-REGISTER.md](./SECURITY-REGISTER.md).

Run the Docker image with `docker run --env-file .env -p 8000:8000
campus-notifier:dev` so the container receives the local Django key. The image
build context excludes `.env`.
