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
| `kern-steering` | Intervention channel (steer / queue / replan / nudge) |
| `kern-orchestration` | Agentic loop (short tasks, context zones, freeze/respawn) |
| `kern-policies` | Permissions, budgets, escalation |
| `kern-skills` | Declarative capability registry |
| `kern-tools` | MCP host |
| `kern-execution` | Sandboxed subprocess runner |
| `kern-guard` | Structural guardrail (inline, blocking) |
| `kern-pii` | PII pseudonymization by ID |
| `kern-scorer` | Semantic guardrail (async) |
| `kern-observation` | Watcher + declared-vs-observed analyzer |
| `kern-vault` | Credentials |

`kern-link` now lives under the org at [kern-ia/kern-link](https://github.com/kern-ia/kern-link).

## Open

- The **core repo name** (`os` vs `kern-os`) is not settled — see the [decision log](decisions.md).
- Non-package repos (this one, the UI app) are exempt from the `kern-*` pattern; the UI's name is decided when it exists.
