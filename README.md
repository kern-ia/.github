# `.github` — Kern org defaults

This repository is the organisation hub for **Kern**. It holds the org profile, the default community health files inherited by every `kern-*` repository, and the org-wide conventions.

## How inheritance works

GitHub treats files in this repo as **fallbacks**: any repository in the org that does not define its own copy of a file automatically uses the one here. A repo that needs something specific defines it locally and the fallback steps aside.

| File | Effect across the org |
|---|---|
| `profile/README.md` | The org landing page at github.com/kern-ia |
| `CONTRIBUTING.md` | Default contribution guide for every repo |
| `CODE_OF_CONDUCT.md` | Default code of conduct |
| `SECURITY.md` | Default security policy |
| `SUPPORT.md` | Default support pointers |
| `.github/ISSUE_TEMPLATE/` | Default issue forms (bug, feature, RFC) |
| `.github/PULL_REQUEST_TEMPLATE.md` | Default PR template |

Not inherited — each repo must carry its own: `LICENSE`, `README.md`, `CODEOWNERS`.

> **Note:** GitHub only activates the profile README, health files, and templates from this repo's **default branch**.

## Contents

- [`profile/README.md`](profile/README.md) — org landing page: what Kern is, package inventory, principles, status.
- Health files and templates, listed above.

Nothing else. This repo holds only what GitHub itself reads and applies across the org. Conventions, design notes and package documentation live in the [wiki](https://github.com/kern-ia/kern-wiki) — GitHub does not read them, so they gain nothing from sitting here and would only fork from the wiki's copy.

## Changing these defaults

Changes here affect every repository in the org that relies on the fallbacks. Open an issue (or an RFC for anything structural) before changing them; typo-level fixes can go straight to a PR.
