# Repository naming convention

**Settled (2026-07): repos use a `<prefix>-<domain>` family.**

The prefix is the product name. The product and the org are being renamed — the current `kern-` is provisional, the convention is not.

## Rules

- Pattern: `<prefix>-<domain>` — lowercase, one hyphen.
- `<domain>` is one word or a clear abbreviation. **The test is legibility, not length**: someone who knows the project should know what the repo does from its name alone. `link`, `orch`, `vault` pass. `svc2`, `common`, `misc` do not.
- **Package repos own exactly one domain**, and the name states which one. Several operations on one subject are still one domain — `kern-anon` detects and pseudonymizes, both acting on PII in text. The question is whether removing an operation would leave the rest with a reason to exist somewhere else.
- **Non-package repos** — apps, utilities, the documentation site — take the prefix too, but not that rule. They only have to have one reason to exist.
- One package repo = one Go module. The module path follows the repo: `github.com/<org>/<prefix>-<domain>`.

## Existing repos

| Repo | Kind | Purpose |
|---|---|---|
| `kern-link` | package | LLM provider gateway — the single passage point to providers |
| `kern-orch` | package | Agentic loop — graph-driven workflows, short tasks, freeze/respawn |
| `kern-anon` | package | PII detection and pseudonymization by ID |
| `kern-ui` | app | Run transitions streamed to a browser |
| `kern-wiki` | docs | Documentation site |
| `.github` | org | Exempt from the pattern — GitHub fixes this name |

Planned packages are listed in the [org profile](../profile/README.md), not here. The decomposition is still moving; a naming convention should not be the thing that freezes it.

## Open

- **The product and org name.** The current one is taken elsewhere. Every `kern-*` repo, module path, and import gets renamed once a replacement is chosen — see the [decision log](decisions.md).
- **The core repo name** (`os` vs `<prefix>-os`).
