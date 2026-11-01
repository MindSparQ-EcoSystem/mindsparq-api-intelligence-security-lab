# Security Policy

## Supported versions

Security support begins when the first implementation release is published. Until then, this repository is a planning/documentation project.

## Reporting a vulnerability

Do not open a public issue containing credentials, exploit details, personal data, or an unpatched vulnerability.

Use GitHub's private vulnerability reporting feature if enabled for this repository, or contact the maintainers through a private channel listed in the organization profile. Do not include live API keys in reports.

## Credential safety rules

- Never commit real credentials, even in tests or examples.
- Use synthetic fixtures such as `sk-test-EXAMPLE_NOT_A_REAL_KEY`.
- Never place raw secrets in logs, telemetry, exception messages, screenshots, or reports.
- Redact matched values before persistence or display.
- Do not test third-party credentials discovered in public repositories.
- Validation is permitted only for credentials entered by an authorized operator or provisioned for a controlled test environment.
- Use the provider's official endpoint and minimum-scope credentials.
- Make potentially billable or quota-consuming checks opt-in and clearly disclose the request before execution.

## Incident response

If a real credential is exposed:
1. Revoke or rotate it immediately at the provider.
2. Review provider usage and billing.
3. Remove it from the repository and relevant history where appropriate.
4. Treat history rewriting as insufficient by itself; assume the credential is compromised.
5. Record the incident without copying the secret into the report.
