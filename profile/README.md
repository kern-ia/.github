# Kern

**OS** — a durable, modular environment for running LLM-based systems, written in Go.

One core binary, `osd`, through which every LLM interaction passes — and a **norm**: manifest schemas that let agents, skills, tools, and providers plug in without touching the core.

## Packages, not modules

The core is not a monolith. It is a **composition root** over independent, reusable Go packages, each living in its own repository and versioned with semver. The core repo contains only the composition root, the norm schemas, migrations, and agent bundles — no domain logic.

Every LLM call follows one fixed hot path:

```
policies-gate → orchestration → guard → pii → kern-link → provider
```

Structural checks (**guard**) block inline. Semantic checks (**scorer**) score asynchronously and never block.

## Package inventory

| Package | Domain | Status |
|---|---|---|
| [kern-link](https://github.com/julienlegoux/kern-proxy) | LLM provider gateway — 35 providers, unified typed event stream, priced model catalog | ✅ exists |
| kern-steering | Intervention channel — steer, queue, replan, nudge | 🔬 planned |
| kern-orchestration | Agentic loop — short tasks, context zones, freeze = fresh-context respawn | 🔬 planned |
| kern-policies | Permissions, budgets, escalation | 🔬 planned |
| kern-skills | Declarative capability registry | 🔬 planned |
| kern-tools | MCP host | 🔬 planned |
| kern-execution | Sandboxed subprocess runner | 🔬 planned |
| kern-guard | Structural guardrail — inline, blocking | 🔬 planned |
| kern-pii | PII pseudonymization by ID (Presidio-based) | 🔬 planned |
| kern-scorer | Semantic guardrail — async, never blocks | 🔬 planned |
| kern-observation | Watcher + declared-vs-observed process analyzer | 🔬 planned |
| kern-vault | Credentials, externalized outside the core | 🔬 planned |

A new package must pass the [brick test](../docs/brick-test.md): the core runs without it, it owns exactly one domain, and plugging it in upgrades the core without modifying any other package.

## Principles

- **Agent ≠ process; agent = data.** Markdown + manifest bundles parameterizing one generic loop.
- **No silent context injection.** Interventions apply at task boundaries or as labeled nudge messages.
- **Credentials live outside the core.** kern-link receives ephemeral credentials per call.
- **GDPR-native.** Anonymization by default; PII pseudonymized before the provider boundary and before persistence; verbatim content never logged by default.
- **Untrusted code runs out-of-process**, capability-sandboxed — skills, tools, external agents.

## Stack

Go core (`CGO_ENABLED=0` static binary) · TypeScript UI (separate app, talks to the core only via steering/observation) · Postgres (journal, budgets; pgvector later) · CI runs offline against kern-link's `faux` provider.

## Status

Design phase — ARCHITECTURE.md v0.3, July 2026. POC milestones: **M0** walking skeleton → **M1** harness → **M2** agents → **M3** supervision.

Org-wide conventions live in [`.github/docs`](../docs): [naming](../docs/naming.md) · [brick test](../docs/brick-test.md) · [versioning](../docs/versioning.md) · [privacy engineering](../docs/privacy-engineering.md) · [decision log](../docs/decisions.md).
