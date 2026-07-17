# Decision log

Lightweight record of org-level decisions: what is settled, what is open. Package-level design decisions belong in their RFCs, not here.

## Settled

| Date | Decision |
|---|---|
| 2026-07 | **Architecture model: packages, not modules.** The core (`osd`) is a composition root over independent semver'd package repos; the core repo carries no domain logic. |
| 2026-07 | **Hot path fixed:** `policies-gate → orchestration → guard → pii → kern-link → provider`. Structural checks block inline; semantic scoring is async and never blocks. |
| 2026-07 | **Repo naming: `kern-*` family** for package repos. See [naming.md](naming.md). |
| 2026-07 | **Shared CI: deferred entirely** until M0 (walking skeleton) defines real needs. Options recorded below so the context isn't lost. |

## Open

### Core repo name — `os` vs `kern-os`
`os` is short but generic (collides mentally with the stdlib package and the concept); `kern-os` is uniform with the family. Decide before the core repo is created.

### License
Posture is *source-available later*: private during design/POC, opened afterwards. All health files are written public-ready. Candidate licenses to evaluate when opening: Apache-2.0 (patent grant, corporate-friendly — usual pick for Go infrastructure), MIT, or a source-available license (BUSL-style) if commercial protection matters. `LICENSE` is not inherited from this repo — every repo needs its own copy once decided.

### Shared CI home (revisit at M0)
The canonical Go CI (vet, lint, test, `CGO_ENABLED=0` build, offline against kern-link's `faux` provider) will be shared across all package repos. Two options, both fine:

- **Reusable workflows in this `.github` repo** — conventional home, no extra repo; tags version CI together with unrelated content.
- **A dedicated `kern-ci` repo** — passes the brick test (own domain, own semver); `.github` keeps only `workflow-templates/` starter stubs (GitHub only supports those here) that call it.

Migration between the two costs one `uses:` line per consuming repo, so starting simple is low-risk.

### UI app repo name
The TypeScript UI (talks to the core only via steering/observation) needs a name when it exists; exempt from `kern-*` or not — undecided.
