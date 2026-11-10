# Security findings register

Record each finding from the Bandit, Gitleaks, Trivy, and Checkov pull-request
checks. Remediated findings remain documented when the underlying value may
still exist in Git history.

| Source | Finding | Disposition | Justification / follow-up | Owner | Revisit by |
|---|---|---|---|---|---|
| Bandit (`B105`, `hardcoded_password_string`) | `SECRET_KEY` was hard-coded in `campus_notifier/settings.py`. | Remediated in the working tree | Django now reads `DJANGO_SECRET_KEY` from the environment. The previous development placeholder remains in Git history; removing it from the file is not rotation. Generate and use a new key for any deployment, and rotate any deployed value that may have reused it. | Application maintainer | 2026-12-10 |
| Trivy (`CVE-2025-69720`) | HIGH in `libncursesw6`, `libtinfo6`, `ncurses-base`, and `ncurses-bin`. | Accepted risk; no fixed versions reported | Trivy reports no fixed version for the Debian 13 packages. Keep the current CRITICAL-only blocking policy and update the base image when Debian publishes fixes. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-119373`) | HIGH in `libsqlite3-0`. | Accepted risk; no fixed version reported | Trivy reports no fixed version for the Debian 13 package. Re-scan on each PR and update when a fixed package is available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-119374`) | HIGH in `libsqlite3-0`. | Accepted risk; no fixed version reported | Trivy reports no fixed version for the Debian 13 package. Re-scan on each PR and update when a fixed package is available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-119379`) | HIGH in `libsqlite3-0`. | Accepted risk; no fixed version reported | Trivy reports no fixed version for the Debian 13 package. Re-scan on each PR and update when a fixed package is available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-16742`) | HIGH in `libsystemd0` and `libudev1`. | Accepted risk; no fixed version reported | Trivy reports no fixed versions for the Debian 13 packages. Re-scan on each PR and update when fixes are available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-54369`) | HIGH in `libacl1`. | Accepted risk; no fixed version reported | Trivy reports no fixed version for the Debian 13 package. Re-scan on each PR and update when a fixed package is available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-76642`) | HIGH across `bsdutils`, `libblkid1`, `liblastlog2-2`, `libmount1`, `libsmartcols1`, `libuuid1`, `login`, `mount`, and `util-linux`. | Accepted risk; no fixed versions reported | Trivy reports no fixed versions for the Debian 13 packages. Re-scan on each PR and update when fixes are available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-78408`) | HIGH across `bsdutils`, `libblkid1`, `liblastlog2-2`, `libmount1`, `libsmartcols1`, `libuuid1`, `login`, `mount`, and `util-linux`. | Accepted risk; no fixed versions reported | Trivy reports no fixed versions for the Debian 13 packages. Re-scan on each PR and update when fixes are available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-78409`) | HIGH across `bsdutils`, `libblkid1`, `liblastlog2-2`, `libmount1`, `libsmartcols1`, `libuuid1`, `login`, `mount`, and `util-linux`. | Accepted risk; no fixed versions reported | Trivy reports no fixed versions for the Debian 13 packages. Re-scan on each PR and update when fixes are available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-78410`) | HIGH across `bsdutils`, `libblkid1`, `liblastlog2-2`, `libmount1`, `libsmartcols1`, `libuuid1`, `login`, `mount`, and `util-linux`. | Accepted risk; no fixed versions reported | Trivy reports no fixed versions for the Debian 13 packages. Re-scan on each PR and update when fixes are available. | Infrastructure maintainer | 2026-12-10 |
| Trivy (`CVE-2026-9538`) | HIGH in `perl-base`. | Accepted risk; no fixed version reported | Trivy reports no fixed version for the Debian 13 package. Re-scan on each PR and update when a fixed package is available. | Infrastructure maintainer | 2026-12-10 |
| Checkov (`CKV_AWS_136`) | ECR repository does not use a customer-managed KMS key. | Accepted risk; suppressed inline in `terraform/main.tf` | ECR encrypts images at rest with AWS-managed AES256 by default. A customer-managed KMS key adds fixed cost and key administration outside this class demo's scope. Reconsider before production use or when customer-managed key controls are required. | Infrastructure maintainer | 2026-12-10 |

Add a separate row for every additional scanner finding. Document the scanner
run or finding identifier and the reason for any accepted risk or suppression.
