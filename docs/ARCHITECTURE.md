# System Architecture

## High-level flow

```text
Operator
  |
  +--> CLI / (later) Local UI
          |
          +--> Authorization & Scope Gate
          |
          +--> Repository Audit Orchestrator
          |       +--> Gitleaks adapter
          |       +--> TruffleHog adapter
          |       +--> Normalizer
          |       +--> Redaction boundary
          |       +--> Sanitized finding store/report
          |
          +--> Provider / Model Catalog
          |       +--> Curated provider metadata
          |       +--> Official documentation references
          |       +--> Refresh and provenance checks
          |
          +--> Owned Credential Validator
                  +--> Protected user input
                  +--> Provider-specific adapter
                  +--> Official minimal auth endpoint
                  +--> Normalized status
```

## Trust boundaries

1. Repository content is untrusted input.
2. Scanner output may contain secrets and must be treated as sensitive until redacted.
3. Provider API responses are external, untrusted data.
4. User-entered credentials are highly sensitive and must not enter logs or persistent reports.
5. The local database is not a credential vault.

## Architectural rules

- Detection and validation are separate subsystems.
- Scanner findings can never be passed automatically to the credential validator.
- Only an explicit user-owned credential input can enter validation.
- Redaction occurs before logging, storage, or rendering.
- Provider metadata is source-attributed and timestamped.
- UI and API layers cannot bypass authorization or validation policy.
