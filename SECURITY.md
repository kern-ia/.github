# Security Policy

## Reporting a vulnerability

**Do not open a public issue for security problems.**

Report privately using **GitHub private vulnerability reporting**: "Report a vulnerability" under the Security tab of the affected repository. It is enabled on every repository in the org, and it gives us a private thread with you.

Include a description, the affected package and version or commit, and reproduction steps if you have them.

You should receive an acknowledgement within a few days. Please allow time for a fix before any public disclosure — we will coordinate timing with you.

## What happens next

The report is triaged, and a fix is prepared privately. When it ships we publish a **GitHub Security Advisory** on the affected repository, and you are **credited in it by name unless you ask us not to be**. Tell us how you want to be named, or that you would rather stay anonymous.

## Scope

All repositories in the Kern org. Reports of particular interest:

- Anything that lets untrusted code (skills, tools, external agents) escape its sandbox or run in-process.
- Credential exposure — credentials must live outside the core; kern-link receives ephemeral credentials per call.
- **Privacy-boundary defects are security issues here.** PII reaching a provider or persistence un-pseudonymized, or verbatim content being logged, is treated with the same severity as a code-execution bug.

## Supported versions

The project is pre-1.0 and in design phase. There are no supported-version guarantees yet: fixes land on the latest 0.x of the affected package only.
