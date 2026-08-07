# Contributing to Kern

This is the org-wide default. Any repository may override it with its own `CONTRIBUTING.md`.

> **Design-phase notice.** The project is pre-1.0. Interfaces, manifests and package boundaries will churn — expect breaking changes between `0.x` minors, and discuss before building anything substantial.

## Where to start

- **Bug?** Open a bug report in the affected repository (Issues → New issue → Bug report). Small, obvious fixes can go straight to a PR.
- **Feature or behavior change?** Open a feature request first, so the owning package and the approach are agreed before code exists.
- **New package, new interface, anything cross-package?** Open an **RFC** issue — see below.

## Proposing a new package

A repo takes seconds to create and is painful to undo, so the decision is made before it exists:

1. **Open an RFC issue.** Name the one domain the package owns, where it sits relative to the hot path, whether it blocks inline or scores async, and what it implies for privacy.
2. **Discuss until the design and the name are both agreed.** Repos are named `<prefix>-<domain>`, lowercase, one hyphen; the domain is one word or a clear abbreviation, judged on whether it says what the repo is.
3. **The repo is created**, and its first README links back to the RFC that produced it.

## Pull requests

- One concern per PR. Link the issue or RFC it resolves.
- Declare the semver impact (patch / minor / major / none) — the template asks for it. Packages are versioned independently; while a package is `0.x`, a minor bump may break and a patch must not.
- **No real personal data anywhere** — code, fixtures, test names, logs, or the PR description itself. Synthetic only.

## Standards and documentation

Each repository carries its own `CONVENTIONS.md`: style, formatting, tests, and what CI enforces. For the repo you are working in, that file is the authority — this guide does not restate it.

Design notes and package documentation live in the [wiki](https://github.com/kern-ia/kern-wiki). Releases are documented in the annotated tag message, which GitHub surfaces as a Release; there is no `CHANGELOG.md`.
