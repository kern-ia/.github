# Contributing to Kern

Thanks for your interest in Kern. This guide is the default for every repository in the org; a repo may override it with its own `CONTRIBUTING.md`.

> **Design-phase notice.** The project is pre-1.0 and in active design (ARCHITECTURE.md v0.3). Interfaces, manifests, and package boundaries will churn. Expect breaking changes between 0.x minors, and discuss before building anything substantial.

## Discussion first

- **Bug?** Open a bug report in the affected repository (Issues → New issue → Bug report). Small, obvious fixes can go straight to a PR.
- **Feature or behavior change?** Open a feature request first so the owning package and approach are agreed before code exists.
- **New package, new interface, anything cross-package?** Open an **RFC** issue — see below.

### Proposing a new package

A repo takes seconds to create and is painful to undo, so the decision is made before it exists:

1. **Open an RFC issue.** Name the one domain the package owns, where it sits relative to the hot path, whether it blocks inline or scores async, and what it implies for privacy.
2. **Discuss until the design and the name are both agreed** — see [naming](docs/naming.md).
3. **The repo is created**, and its first README links back to the RFC that produced it.

## Code standards (Go)

- `gofmt` and `go vet` clean — no exceptions.
- The build must pass with `CGO_ENABLED=0`. The core ships as a static binary; packages must not break that.
- Prefer table-driven tests; keep packages small and focused on their one domain.
- **Tests must run offline.** No live provider calls in tests or CI — kern-link's `faux` provider is the target for anything touching the LLM boundary.
- **No real personal data** in code, fixtures, test names, or logs. See [privacy engineering](docs/privacy-engineering.md).

## Pull requests

- One concern per PR. Small PRs get reviewed; large ones get postponed.
- Link the issue or RFC the PR resolves.
- Declare the semver impact (patch / minor / major / none) — the template asks for it. See [versioning](docs/versioning.md).
- Write commit messages in the imperative, scoped to what changed ("add freeze respawn to orchestration loop"). [Conventional Commits](https://www.conventionalcommits.org) style is welcome but not required.

## What gets merged

Maintainers merge PRs that: solve an agreed problem, stay inside their package's domain, consume other packages only through the norm rather than reaching into their internals, and leave CI green offline.
