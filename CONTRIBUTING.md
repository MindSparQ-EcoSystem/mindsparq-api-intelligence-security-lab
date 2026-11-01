# Contributing

Thank you for helping improve MAISL.

## Before contributing

- Read the README, PRD, TRD, and SECURITY policy.
- Keep the project local-first and lightweight.
- Preserve the authorization boundary: no third-party credential testing or harvesting.
- Prefer small, testable changes over broad rewrites.
- Do not add paid-service dependencies to the core path.

## Development expectations

- Use type hints and clear module boundaries.
- Add tests for new detection rules and provider adapters.
- Use synthetic credentials only.
- Do not add real tokens to fixtures, logs, screenshots, or documentation.
- Make network calls explicit, bounded, and documented.
- Handle rate limits, timeouts, retries, and provider errors safely.
- Cite official provider documentation for provider-specific behavior.

## Pull requests

Include:
- Problem and proposed change.
- Security and privacy impact.
- Tests run and their results.
- Any new network permissions or data collection.
- Documentation updates.

Do not claim a test passed unless it was actually run.
