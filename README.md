# CREANODE CI

Central, versioned reusable GitHub Actions workflows for CREANODE repositories.

## Security gate

Caller repositories use .github/workflows/security.yml to call:

staafnet/creanode-ci/.github/workflows/security-reusable.yml@main

The reusable gate provides:
- Trivy repository scanning for HIGH/CRITICAL vulnerabilities, misconfiguration and secrets;
- Semgrep Community Edition SAST with security-audit and OWASP Top 10 rules;
- optional build + Trivy scan of the production Docker image;
- non-blocking Trivy license inventory for policy visibility.

Security tool and Action versions are pinned centrally. Product repositories should not duplicate scanner implementation.

## Legacy-debt adoption

Repositories with pre-existing HIGH/CRITICAL findings may receive a centrally managed baseline under `baselines/<repo>.trivyignore.yaml`. Baselines are generated from the first adoption scan, are outside the caller repository, and use an expiry date. They suppress only the listed historical finding IDs; new HIGH/CRITICAL findings still fail the gate. On expiry, unresolved baseline entries become blocking again.

Caller repositories cannot weaken this baseline from their own pull requests.
