# Test and Acceptance Plan

## Test layers

1. Unit tests: parsers, normalizers, redaction, provider response classification.
2. Integration tests: external scanner invocation using synthetic repositories.
3. Adapter tests: mocked provider responses; live tests only with explicit opt-in and user-owned test credentials.
4. Security tests: log/report/database leakage, authorization bypass, unsafe command execution.
5. Platform tests: supported Ubuntu and Windows environments.
6. Performance tests: large repository, bounded memory, cancellation, timeout.

## Required synthetic cases

- Valid-looking but fake provider key patterns.
- Similar strings that should not match.
- Secret split across line boundaries (where scanner supports it).
- Secret in historical commit.
- Secret in filename and environment file.
- Multiple findings in one file.
- Binary/large file exclusions.
- Malicious filenames and unusual Unicode.
- Scanner timeout and non-zero exit.
- Provider 401/403/429/5xx and timeout responses.

## Acceptance criteria

- [ ] Local scan requires no cloud account.
- [ ] Remote scan requires explicit authorization confirmation.
- [ ] No raw secret is written to stdout, stderr, logs, JSON, CSV, or SQLite.
- [ ] Scanner output is redacted before persistence.
- [ ] Scanner findings cannot be sent to the validator.
- [ ] Validation accepts only explicit operator-owned credential input.
- [ ] User sees endpoint and possible quota/cost before a validation request.
- [ ] Authentication success is not presented as proof of model access or remaining quota.
- [ ] Every provider/model record includes official source and checked timestamp.
- [ ] Rate limits and timeouts are handled without aggressive retries.
- [ ] Tests use synthetic secrets only.
- [ ] Documentation clearly states unsupported cases and limitations.

## Evidence rule

Record exact commands, environment, and results. Never claim a test passed unless it was executed successfully.
