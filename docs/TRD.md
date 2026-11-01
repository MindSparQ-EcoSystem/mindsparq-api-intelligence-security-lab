# Technical Requirements Document (TRD)

## 1. Initial technical direction

Build a Python CLI-first application. Add a local API or UI only after the core scanning and validation workflows are stable.

Recommended baseline:
- Python 3.12+ (verify dependency support before selecting exact minimum).
- Typer or argparse for CLI.
- Pydantic for normalized schemas.
- SQLite for local metadata.
- HTTPX for official provider API calls.
- pytest for tests.
- Ruff for lint/format.
- Gitleaks and TruffleHog as optional external tools, not silently bundled until license review.

## 2. Module boundaries

```text
maisl/
  cli/
  core/
    config.py
    authorization.py
    redaction.py
    results.py
  scanners/
    base.py
    gitleaks.py
    trufflehog.py
    git_native.py
  providers/
    registry.py
    base.py
    adapters/
  models/
    catalog.py
    sources.py
  storage/
    sqlite.py
  reporting/
    json_report.py
    csv_report.py
  scheduling/
  tests/
```

## 3. Normalized finding schema

A finding may contain:
- finding_id
- repository identifier (not credentials)
- file path or commit reference
- detector name and version
- credential type / provider guess
- confidence
- masked fingerprint (non-reversible; avoid storing raw value)
- first_seen / last_seen
- remediation status

Never persist the raw matched secret. Avoid storing a reversible encrypted copy: the scanner does not need it.

## 4. Credential validation contract

Validation input must originate from a protected operator input flow, not from scanner findings.

Adapter interface should expose:
- provider_id
- supported_auth_check
- endpoint and official documentation reference
- required scopes/permissions
- whether request may consume quota or incur cost
- timeout and retry policy
- normalized response classifier

Possible result states:
- AUTHENTICATED
- INVALID_CREDENTIAL
- INSUFFICIENT_PERMISSION
- RATE_LIMITED
- QUOTA_EXHAUSTED
- PROVIDER_UNAVAILABLE
- UNSUPPORTED_CHECK
- UNKNOWN

Do not claim model availability or quota from authentication success. Model access must be a separate, explicit, low-impact check where supported.

## 5. Provider/model catalog

Each provider/model record should include:
- stable internal ID
- display name
- official provider URL
- API documentation URL
- model identifier (if applicable)
- API compatibility notes
- free-tier status: FREE, PAID, LIMITED_FREE, TRIAL, UNKNOWN
- pricing URL and checked_at timestamp
- availability source and checked_at timestamp
- deprecation status
- source confidence

Do not hard-code claims as timeless facts. Provider terms can vary by region, account, and date.

## 6. Network behavior

- HTTPS only.
- Explicit connect/read timeouts.
- Bounded retries with exponential backoff and jitter.
- Respect Retry-After and provider rate limits.
- No broad endpoint probing.
- No arbitrary model generation during credential validation.
- Redact authorization headers and request bodies from logs.
- Use official provider endpoints only.

## 7. Storage

SQLite stores metadata and sanitized findings only. Secrets are not stored. Local database file permissions should be restrictive. Provide a purge command and retention configuration.

## 8. Performance

- CLI-first, low idle resource use.
- Bounded worker count; default conservative.
- Stream large Git outputs rather than loading all history into memory.
- Cancellation support.
- Configurable scan depth and file-size limits.
- No mandatory background daemon.

## 9. Interfaces

MVP: CLI.  
Later: optional local-only FastAPI service and React dashboard, bound to localhost by default with authentication/CSRF protections if browser-accessible.

## 10. Compatibility and packaging

Target Linux and Windows first; macOS may follow. Use standard Python packaging and avoid Docker as a requirement. Validate platform-specific scanner installation and path handling.
