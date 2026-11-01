# Security Design and Threat Model

## Assets

- User-owned API credentials.
- Source code and repository metadata.
- Sanitized findings and remediation status.
- GitHub access tokens.
- Provider/model metadata.

## Threat actors and failure modes

- Accidental secret exposure by a developer.
- Malicious repository content or prompt-injection-like text in files.
- Log/report leakage.
- Unauthorized scanning or credential testing.
- Compromised dependency or scanner binary.
- Excessive provider requests causing quota/cost impact.
- False positive or false negative detection.

## Mandatory controls

### Authorization
- Require the operator to attest that they own or are authorized to scan each remote repository.
- Prefer local clone scanning.
- Use minimum GitHub scopes and short-lived credentials where possible.
- Do not crawl public repositories to collect credentials.

### Secret handling
- Treat raw scanner matches as tainted sensitive data.
- Redact before persistence, output, telemetry, or exception handling.
- Never persist raw secrets or reversible copies.
- Avoid command-line arguments for secrets because process listings may expose them.
- Use OS keyring or protected prompt for user-owned credentials.

### Validation
- Accept only user-entered credentials or controlled test credentials.
- Require explicit confirmation before network requests.
- Show endpoint, data sent, and possible quota/cost effect.
- Use official documented endpoints.
- No automatic validation of repository findings.
- No bulk validation.

### Supply chain
- Pin dependencies.
- Review licenses and provenance of scanner tools.
- Verify release checksums/signatures where available.
- Keep external scanner execution least-privileged and bounded.

### Reporting
- Mask credential values.
- Avoid printing full file lines when they may contain secrets.
- Include repository, path, commit, detector, and remediation—not raw value.
- Restrict local report file permissions.

## Abuse cases explicitly prohibited

- Harvesting exposed third-party keys.
- Testing whether someone else's key works.
- Enumerating accounts, models, or quota using discovered credentials.
- Building a public index of usable credentials.
- Bypassing provider rate limits or access controls.

## Security acceptance criteria

- Automated tests prove raw secrets do not appear in reports, logs, exceptions, or database rows.
- Validator cannot be invoked from scanner finding objects.
- Unauthorized remote scans are blocked before network access.
- Every adapter documents its endpoint and quota impact.
- No secret is included in crash telemetry (telemetry is off by default).
