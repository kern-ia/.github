# Security Policy

## Reporting a vulnerability

**Do not open a public issue for security problems.**

Report privately:

- Preferred: GitHub **private vulnerability reporting** ("Report a vulnerability" under the Security tab of the affected repository), where enabled.
- Otherwise: email **lgx.julien@gmail.com** with a description, affected package and version/commit, and reproduction steps if you have them.

You should receive an acknowledgement within a few days. Please allow time for a fix before any public disclosure — we will coordinate timing with you.

## Scope

All repositories in the Kern org. Reports of particular interest:

- Anything that lets untrusted code (skills, tools, external agents) escape its sandbox or run in-process.
- Credential exposure — credentials must live outside the core; kern-link receives ephemeral credentials per call.
- **Privacy-boundary defects are security issues here.** PII reaching a provider or persistence un-pseudonymized, or verbatim content being logged, is treated with the same severity as a code-execution bug. See [privacy engineering](https://github.com/kern-ia/.github/blob/main/docs/privacy-engineering.md).

## Supported versions

The project is pre-1.0 and in design phase. There are no supported-version guarantees yet: fixes land on the latest 0.x of the affected package only.
