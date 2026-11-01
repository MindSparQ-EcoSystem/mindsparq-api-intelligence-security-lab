# Product Requirements Document (PRD)

## 1. Product summary

MindSparQ API Intelligence & Security Lab (MAISL) is a free/open-source, local-first developer tool. It combines authorized repository secret auditing with an independently maintained AI provider/model catalog and safe validation of operator-owned API credentials.

## 2. Problem

New and intermediate developers frequently:
- accidentally commit API keys into source code or Git history;
- do not know which provider a credential belongs to;
- confuse a key's apparent format with actual authentication;
- lack a reliable, current view of model availability, API compatibility, pricing, and free-tier conditions;
- struggle to remediate exposed credentials safely.

Existing scanners solve much of secret detection. MAISL should integrate mature scanners rather than recreate their detection engines, then add accessible provider/model intelligence and safe, owner-controlled validation.

## 3. Target users

- Beginner and intermediate developers / vibe coders.
- Students and educators teaching secure development.
- Independent developers and small teams.
- Open-source maintainers auditing repositories they control.

## 4. Goals

1. Scan only repositories the operator owns or is authorized to assess.
2. Detect likely secrets in working trees and Git history using established scanners.
3. Identify likely provider/credential type without exposing the value.
4. Produce actionable remediation guidance.
5. Validate only operator-supplied, operator-owned credentials using official provider APIs.
6. Maintain a source-attributed catalog of AI providers and models.
7. Run locally with minimal resource use and no mandatory paid service.

## 5. Non-goals

- Harvesting public third-party credentials.
- Testing or using credentials found in public repositories without owner authorization.
- Publishing a searchable database of exposed keys.
- Exploiting accounts, bypassing quotas, or probing provider systems at scale.
- Guaranteeing complete coverage of GitHub or all secret formats.
- Replacing GitHub Advanced Security or commercial secret-management platforms.

## 6. Core user journeys

### A. Audit my repository
1. User selects a local repository or supplies an authorized repository URL.
2. App explains required access and scan scope.
3. User confirms authorization.
4. Scanner runs with bounded resource settings.
5. Findings are redacted before persistence.
6. User receives file/commit location, detector, confidence, and remediation.
7. User rotates/revokes affected credentials at the provider.

### B. Validate my API key
1. User selects a provider.
2. User enters their own key into a protected input.
3. App explains the exact endpoint, request, possible quota/cost impact, and data sent.
4. User explicitly confirms.
5. Adapter makes the smallest documented authentication check.
6. App reports authentication status separately from model access, quota, and rate limits.
7. Raw key is discarded from process memory as soon as practical and never saved in reports/logs.

### C. Research provider/model information
1. App refreshes provider/model metadata from official sources or maintained curated records.
2. Each record includes source URL and last-checked date.
3. Free-tier and pricing claims are qualified and linked to provider terms.
4. Stale or unavailable information is marked accordingly.

## 7. Functional requirements

- FR-01: Accept local Git repository paths.
- FR-02: Support remote repositories only after authorization confirmation.
- FR-03: Scan working tree and Git history.
- FR-04: Integrate Gitleaks and/or TruffleHog as optional scanner backends.
- FR-05: Normalize findings into a common schema.
- FR-06: Mask secrets before any output or persistence.
- FR-07: Classify provider and credential type with confidence.
- FR-08: Provide remediation steps, including revoke/rotate.
- FR-09: Accept operator-owned credentials through secure input.
- FR-10: Provide provider-specific, official-endpoint validation adapters.
- FR-11: Separate authentication, model access, quota, and rate-limit states.
- FR-12: Maintain a provider/model registry with source provenance.
- FR-13: Export sanitized JSON and CSV reports.
- FR-14: Support local scheduled scans only for configured authorized repositories.
- FR-15: Provide cancellation, timeout, and rate-limit handling.

## 8. Non-functional requirements

- NFR-01: Local-first operation; no telemetry by default.
- NFR-02: No raw secret persistence.
- NFR-03: Least-privilege GitHub scopes.
- NFR-04: Explicit consent for network calls and potentially billable validation.
- NFR-05: Lightweight baseline suitable for modest laptops.
- NFR-06: Deterministic tests with synthetic fixtures.
- NFR-07: Clear unknown/unsupported states; no false certainty.
- NFR-08: Accessible CLI output; dashboard is a later phase.

## 9. Success metrics

- Detection precision/recall measured against synthetic, licensed test corpora.
- 100% of persisted sample findings contain redacted values only.
- 0 real credentials in test fixtures and CI logs.
- Provider adapter tests verify expected success, invalid-key, quota, rate-limit, timeout, and server-error states.
- User can complete a local repository scan without creating a cloud account.
- Every provider/model fact has provenance and freshness metadata.

## 10. Open decisions

- Final CLI command structure.
- Exact supported Python versions.
- Whether the first release includes a local web UI or CLI only.
- Which provider adapters are included in MVP.
- License and ownership approval by MindSparQ maintainers.
