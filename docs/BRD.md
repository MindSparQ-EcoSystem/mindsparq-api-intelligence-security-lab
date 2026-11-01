# Business Requirements Document (BRD)

## Purpose

Provide a free, transparent developer-security and AI-provider research utility for learners, independent developers, educators, and small teams.

## Value proposition

MAISL reduces accidental credential exposure and helps users make informed choices about AI providers and models without requiring a paid SaaS account.

## Stakeholders

- Product owner: MindSparQ-EcoSystem maintainers.
- Primary users: developers, students, educators, open-source maintainers.
- External dependencies: GitHub and AI provider APIs/documentation.
- Upstream projects: Gitleaks, TruffleHog, and other integrations, subject to license compatibility.

## Operating model

- Free and open-source distribution.
- Local-first core.
- No sale, brokerage, or redistribution of credentials.
- Optional donations or sponsorship may support maintenance, but must not gate core security features.
- Provider catalog maintenance should be community-reviewable and source-attributed.

## Constraints

- Public API availability, pricing, and free-tier policies change frequently.
- Provider APIs may impose rate limits or quota charges.
- GitHub search/indexing is not exhaustive.
- Third-party scanner licenses and notices must be reviewed before bundling or redistributing binaries.
- Maintainer capacity is limited; MVP scope must remain small.

## Risks and mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Secret appears in logs/report | Critical | Redact at detection boundary; test redaction |
| Unauthorized repository scan | High | Authorization confirmation and documented scope |
| Accidental third-party key testing | Critical | Validator accepts only operator-entered credentials |
| Provider API costs | Medium/High | Explicit consent, low-cost check, no default model generation |
| Stale model/pricing data | Medium | Source URL and last-checked timestamp |
| False positives | Medium | Confidence levels and suppressions |
| Upstream license incompatibility | High | Dependency/license review before bundling |
| Resource-heavy scans | Medium | Bounded workers, cancellation, configurable history depth |

## Business acceptance

The project is ready for an MVP release only when security boundaries, redaction, local-first behavior, provider provenance, and tests are demonstrated—not merely documented.
