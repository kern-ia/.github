# Repository naming convention

**Settled (2026-07): package repos use the `kern-*` family.**

## Rules

- Pattern: `kern-<domain>` — lowercase, hyphen after the prefix, one word for the domain wherever possible.
- The `<domain>` names the single domain the package owns (see the [brick test](brick-test.md)): `kern-guard`, `kern-vault`, `kern-steering`.
- One repo = one package = one Go module. Module path follows the repo:
  `github.com/kern-ia/kern-<domain>`.
  Prefer the lowercase org slug in module paths — GitHub resolves it case-insensitively, and lowercase avoids the Go module proxy's `!p`-style escaping of uppercase letters.

## Target repo list

| Repo | Domain |
|---|---|
| `kern-link` | LLM provider gateway (single passage point to providers) |
| `kern-orch` | Agentic loop (short tasks, context zones, freeze/respawn) |
| `kern-anon` | PII detection and pseudonymization by ID |
| `kern-ui` | Interface brick (run transitions streamed to a browser) |
| `kern-steering` | Intervention channel (steer / queue / replan / nudge) |
| `kern-policies` | Permissions, budgets, escalation |
| `kern-skills` | Declarative capability registry |
| `kern-tools` | MCP host |
| `kern-execution` | Sandboxed subprocess runner |
| `kern-guard` | Structural guardrail (inline, blocking) |
| `kern-scorer` | Semantic guardrail (async) |
| `kern-observation` | Watcher + declared-vs-observed analyzer |
| `kern-vault` | Credentials |

The first four exist; the rest are planned. `kern-orch` and `kern-anon` are the settled names — earlier drafts called them `kern-orchestration` and `kern-pii`. Short domain words win.

`kern-link` now lives under the org at [kern-ia/kern-link](https://github.com/kern-ia/kern-link).

## Open

- The **core repo name** (`os` vs `kern-os`) is not settled — see the [decision log](decisions.md).

Non-package repos took the prefix anyway: the UI shipped as `kern-ui` and the documentation site as `kern-wiki`. Only this `.github` repo is exempt, and only because GitHub forces the name.
