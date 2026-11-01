# Data Handling and Privacy Policy

## Default posture

MAISL is local-first. No telemetry or remote reporting is enabled by default.

## Data categories

| Data | Default handling |
|---|---|
| Repository path | Local only |
| Repository URL | Local config/history only if user opts in |
| File/commit location | Sanitized local finding |
| Raw secret value | Never persist; redact immediately |
| Masked secret | Optional, sanitized evidence only |
| User-owned API key | Transient validation input; optional OS keyring only if user explicitly saves |
| Provider/model metadata | Local cache with source and timestamp |
| Logs | No credentials, authorization headers, or secret-bearing lines |

## Retention

- Findings remain local until user deletes them.
- Provide a purge function.
- Do not upload reports automatically.
- User-initiated export must be sanitized.

## Future network features

Any future hosted service must have a separate privacy review, explicit opt-in, documented retention, deletion controls, and a clear data-processing notice. It must not receive raw credentials.
