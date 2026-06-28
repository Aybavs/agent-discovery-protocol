# Security Policy

This project is currently a working-draft specification and does not yet define a production protocol or reference implementation.

Security feedback is still highly valuable.

## What to report

Please open a security-related issue or contact the maintainer if you identify:

- discovery metadata risks,
- spoofing or integrity risks,
- information disclosure risks,
- authorization confusion,
- prompt injection risks,
- tool poisoning risks,
- malicious metadata risks,
- privacy concerns,
- unsafe assumptions in the specification language.

## Current security principles

The current drafts follow these principles:

1. Discovery does not imply authorization.
2. Descriptive metadata must not be treated as trusted instructions.
3. Operators must control what is made discoverable.
4. Discovery should not duplicate authoritative interface definitions.
5. Discovery consumers should ignore unknown fields safely.
6. Trust and signatures should be considered separate extension areas.

## Reporting channel

A dedicated security reporting channel is **not yet configured**.

For non-sensitive specification concerns, please open a **public issue**.

For sensitive concerns, please do not include sensitive details in public issues. Instead, contact the maintainer through [GitHub profile contact methods](https://github.com/Aybavs) until a dedicated reporting channel is configured.

## Responsible disclosure

Because this project is currently a specification draft, most issues can be discussed publicly.

If a future reference implementation or hosted service is added, this policy will be updated with private reporting instructions.
