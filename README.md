# `.github` — Kern org defaults

This repository is the organisation hub for **Kern**. It holds the org profile, the default community health files inherited by every `kern-*` repository, and the org-wide conventions.

## How inheritance works

GitHub treats files in this repo as **fallbacks**: any repository in the org that does not define its own copy of a file automatically uses the one here. A repo that needs something specific defines it locally and the fallback steps aside.

| File | Effect across the org |
|---|---|
| `profile/README.md` | The org landing page at github.com/Project-Kern |
| `CONTRIBUTING.md` | Default contribution guide for every repo |
| `CODE_OF_CONDUCT.md` | Default code of conduct |
| `SECURITY.md` | Default security policy |
| `SUPPORT.md` | Default support pointers |
| `.github/ISSUE_TEMPLATE/` | Default issue forms (bug, feature, RFC) |
| `.github/PULL_REQUEST_TEMPLATE.md` | Default PR template |

Not inherited — each repo must carry its own: `LICENSE`, `README.md`, `CODEOWNERS`.

> **Note:** GitHub only activates the profile README, health files, and templates from this repo's **default branch**.

## Contents

- [`profile/README.md`](profile/README.md) — org landing page: what OS is, package inventory, principles, status.
- [`docs/`](docs/) — org-wide conventions:
  - [naming.md](docs/naming.md) — the `kern-*` repository naming convention
  - [brick-test.md](docs/brick-test.md) — the gate a new package must pass, and the process to propose one
  - [versioning.md](docs/versioning.md) — semver and release policy for package repos
  - [privacy-engineering.md](docs/privacy-engineering.md) — GDPR (RGPD) rules as engineering constraints
  - [decisions.md](docs/decisions.md) — decision log: what is settled, what is open
- Health files and templates listed above.

## Changing these defaults

Changes here affect every repository in the org that relies on the fallbacks. Open an issue (or an RFC for anything structural) before changing conventions; typo-level fixes can go straight to a PR.
