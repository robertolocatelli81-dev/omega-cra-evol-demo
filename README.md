# cra-evidence-demo

From 11 September 2026, a manufacturer that learns of an actively exploited vulnerability in its product must notify
it within 24 hours, follow up within 72 hours and send a final report (EU Cyber Resilience Act, Regulation (EU)
2024/2847, Art. 14). [cra-evidence](https://github.com/robertolocatelli81-dev/cra-evidence) keeps the SBOM, the
Art. 14 clock and the notices in one hash-chained ledger that anyone can verify offline.

This repository shows it installed the three ways you would install it, on clean GitHub-hosted runners, every week
([`installable.yml`](.github/workflows/installable.yml)). Each job verifies the evidence pack signed and published with
the release:

| Job | Install | Before running |
|---|---|---|
| `pip` | `pip install --index-url https://robertolocatelli81-dev.github.io/pypi/ cra-evidence` | release files checked against `SHA256SUMS`; a tampered pack must fail |
| `image` | `docker run ghcr.io/robertolocatelli81-dev/cra-evidence:0.9.0` | `gh attestation verify`: built by the release workflow, at the release tag |
| `action` | `uses: robertolocatelli81-dev/cra-evidence@v0.9.0` | the action verifies the provenance of the image digest it pulled, then runs it without network |

Copy the job you need into your own workflow and replace the release's pack with yours.

Not a conformity assessment, not CE marking, not the official CSIRT/ENISA reporting channel.

Licence: Apache-2.0 (this demo; cra-evidence itself is AGPL-3.0-or-later).
