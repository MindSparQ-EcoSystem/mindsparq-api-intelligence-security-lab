# Roadmap

## Stage 0 — Project foundation
- [ ] Confirm repository name, visibility, license, and maintainers.
- [ ] Publish project scope and security boundaries.
- [ ] Add contribution and vulnerability-reporting guidance.
- [ ] Review upstream licenses and integration options.

## Stage 1 — Local scanner MVP
- [ ] Python package and CLI skeleton.
- [ ] Local repository authorization/scope confirmation.
- [ ] Gitleaks adapter.
- [ ] TruffleHog adapter (optional, license and execution review first).
- [ ] Normalized finding schema.
- [ ] Mandatory redaction boundary.
- [ ] Sanitized JSON/CSV reports.
- [ ] Synthetic fixture test suite.

## Stage 2 — Provider intelligence
- [ ] Provider registry schema.
- [ ] Official-source metadata for initial providers.
- [ ] Model catalog and compatibility notes.
- [ ] Free/paid/trial classification with source timestamps.
- [ ] Staleness indicators.

## Stage 3 — Owned-key validation
- [ ] Protected credential input.
- [ ] Explicit consent and quota/cost disclosure.
- [ ] Provider adapter interface.
- [ ] One or two initial official auth checks.
- [ ] Separate auth/model/quota/rate-limit statuses.
- [ ] Redaction and no-persistence tests.

## Stage 4 — Usability
- [ ] Guided remediation workflow.
- [ ] Configurable local scheduling.
- [ ] Lightweight local dashboard only if CLI feedback justifies it.
- [ ] Windows and Ubuntu packaging.

## Stage 5 — Release readiness
- [ ] Security review.
- [ ] Dependency and license review.
- [ ] Threat-model verification.
- [ ] Documentation and reproducible release.
- [ ] Community beta and issue templates.

## Release rule

Do not label the product production-ready until all security acceptance criteria and platform-specific tests pass.
