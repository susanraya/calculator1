# calculator1 — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
create a simple calculator

**Documentation version:** v1
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 1 entry |
| [Development](development/README.md) | 1 entry |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | not generated yet |
| [API (OpenAPI)](architecture/api/openapi.yaml) | not generated yet |
| [Decisions (ADRs)](architecture/adr/README.md) | 0 decisions |
| [Sprint plan](development/sprint-plan.md) | not generated yet |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 13 requirements |
| [Changelog](CHANGELOG.md) | 1 version |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Stack is approved but no architecture artifact exists yet that maps these components into an actual component/deployment design.
- NFR-005 is an accepted-risk limitation: full WCAG/GIGW accessibility conformance beyond the basics (keyboard, focus, contrast) is explicitly out of scope — confirm this is acceptable for the target user base, including users with disabilities beyond these basics.
- This 'DPDP does not materially apply' assumption is stated in the requirements but has not been independently reviewed or signed off by a compliance owner.
- Verifiable parental consent / no tracking-or-targeted-advertising-to-children provisions of DPDP are not addressed by any requirement (plausibly not applicable since no data is collected at all, but not explicitly confirmed).
- Breach notification duties (DPDP Act notification to the Data Protection Board and affected people; CERT-In 6-hour incident reporting and 180-day ICT log retention) are not addressed by any requirement, even though the app will run on AWS infrastructure.

### Architecture

- Architecture phase has not started, or no design documents/diagrams/ADRs were provided: component design, deployment topology (e.g., CloudFront/S3/FastAPI layout), and data flow are undocumented.

### Development

- Development phase has not started, or no planning/implementation records were provided: cannot confirm which user stories or acceptance criteria have been built.

### Testing

- Testing phase has not started: none of AC-001 through AC-024 has recorded verification results.

### Deployment

- No deployment recorded yet: it is unconfirmed whether the approved AWS/CloudFront hosting for the static FastAPI-served React app has been provisioned or released.

### Maintenance

- No maintenance notes available; this is expected since the application has not yet been recorded as deployed.
<!-- sdlc:auto:end open-gaps -->
