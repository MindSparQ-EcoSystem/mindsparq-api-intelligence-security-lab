# MindSparQ API Intelligence & Security Lab (MAISL)

> Open-source, local-first tooling for AI provider/model intelligence and **authorized** repository secret auditing.

**Status:** Project definition / documentation starter — implementation has not started.  
**Organization:** MindSparQ-EcoSystem  
**Proposed repository:** `mindsparq-api-intelligence-security-lab`  
**License:** Apache-2.0 (proposed; confirm before publishing)

## Mission

Help developers, students, educators, and small teams understand AI API providers and models, audit repositories they own or are authorized to assess, and safely validate credentials they control.

MAISL is not a public credential-harvesting service. It must never collect, store, test, publish, or redistribute third-party exposed credentials. Public-repository research must use metadata and non-secret evidence, with secret values redacted at source.

## Project principles

- **Authorization first:** scan only repositories the operator owns or has explicit permission to assess.
- **No credential harvesting:** do not build a database of working third-party keys.
- **Local-first:** default to local processing and SQLite; no mandatory cloud service.
- **Least privilege:** use read-only GitHub access where possible.
- **No secret persistence:** never store raw credentials in reports, logs, telemetry, fixtures, or the database.
- **Provider-specific truth:** distinguish key-format checks, authentication, model access, quota, and rate limits.
- **Evidence over assumptions:** unknown means unknown; never infer a key is valid from its format.
- **Free and open source:** community-oriented, transparent, and usable without paid subscriptions.

## Planned capabilities

1. Authorized Git repository scanning (working tree and history).
2. Secret detection through established tools such as Gitleaks and TruffleHog, subject to their licenses and safe integration boundaries.
3. Provider identification using maintained, reviewed detection rules.
4. Secure validation of **user-supplied, user-owned** credentials through official provider APIs.
5. AI provider/model catalog with official documentation, API compatibility, pricing links, and free-tier notes.
6. Local reports with masked evidence and remediation guidance.
7. Scheduled scans of explicitly authorized repositories.

## What MAISL will not do

- Search the public internet for working third-party API keys.
- Test, replay, exploit, or use credentials found in repositories without authorization from their owner.
- Provide bulk credential harvesting, credential ranking, key sharing, or public key databases.
- Attempt quota-consuming model calls without explicit operator consent.
- claim complete GitHub coverage or guaranteed detection.

## Current project status

This repository starter contains planning and governance documents only. No scanner, API validator, dashboard, or scheduled research service is implemented yet.

## Documentation

- [Product Requirements](docs/PRD.md)
- [Business Requirements](docs/BRD.md)
- [Technical Requirements](docs/TRD.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Security and Threat Model](docs/SECURITY.md)
- [Data Handling Policy](docs/DATA_POLICY.md)
- [Provider Registry Design](docs/PROVIDER_REGISTRY.md)
- [Roadmap](docs/ROADMAP.md)
- [Test and Acceptance Plan](docs/TEST_PLAN.md)
- [Contributing](CONTRIBUTING.md)
- [Security reporting](SECURITY.md)

## Proposed technology

- Python 3.12+ (confirm supported versions during implementation)
- FastAPI only if/when an API service is needed
- SQLite for local metadata
- HTTPX for provider API adapters
- Gitleaks / TruffleHog as optional external scanners
- React + TypeScript dashboard only after the CLI/core is proven

Avoid mandatory Docker, cloud databases, or paid APIs in the initial release.

## Quick start

There is no runnable application in this documentation-only starter. Follow the roadmap and implementation plan before publishing a versioned release.

## License

Apache License 2.0. See [LICENSE](LICENSE).
