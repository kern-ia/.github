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

| Package | Domain |
|---|---|
| [kern-link](https://github.com/kern-ia/kern-link) | LLM provider gateway — 35 providers, unified typed event stream, priced model catalog |
| [kern-orch](https://github.com/kern-ia/kern-orch) | Agentic loop — graph-driven workflows, short tasks, context zones, freeze = fresh-context respawn |
| [kern-anon](https://github.com/kern-ia/kern-anon) | PII detection and pseudonymization by ID — a Go rewrite of Presidio's core |
| [kern-ui](https://github.com/kern-ia/kern-ui) | Interface brick — streams run transitions to a browser |
| [kern-exec](https://github.com/kern-ia/kern-exec) | Sandboxed process execution — filesystem allow-list, network denied unless granted, wall-clock timeout |
| [kern-firewall](https://github.com/kern-ia/kern-firewall) | Agnostic AI firewall — a chokepoint in front of every request and action directed at an AI provider, agent or not |
| [kern-memory](https://github.com/kern-ia/kern-memory) | Where other `kern-*` bricks put things they need to remember |
| [kern-notify](https://github.com/kern-ia/kern-notify) | Relays run streams to Telegram, and lets that same chat steer a run back |
| [kern-billing](https://github.com/kern-ia/kern-billing) | Real AI cost to end-user token wallet — Stripe subscriptions, monthly-reset credits, non-expiring top-ups |

Nine further bricks are planned: steering, policies, skills, tools, execution, guard, scorer, observation and vault. Their boundaries are still moving — the [wiki](https://github.com/kern-ia/kern-wiki) carries the current thinking.

Alongside them sit [kern-wiki](https://github.com/kern-ia/kern-wiki), the documentation site, and this [`.github`](https://github.com/kern-ia/.github) repo, which holds the org profile and the health files every repo inherits.

A new package owns exactly one domain, plugs in through the norm without any other package being modified, and is proposed as an RFC before its repo exists — see [contributing](https://github.com/kern-ia/.github/blob/main/CONTRIBUTING.md).

## Principles

- **Agent ≠ process; agent = data.** Markdown + manifest bundles parameterizing one generic loop.
- **No silent context injection.** Interventions apply at task boundaries or as labeled nudge messages.
- **Credentials live outside the core.** kern-link receives ephemeral credentials per call.
- **Privacy by architecture.** Personal data is pseudonymized before the provider boundary and before persistence; verbatim prompt and completion text is never logged by default.
- **Untrusted code runs out-of-process**, capability-sandboxed — skills, tools, external agents.

## Stack

Go core (`CGO_ENABLED=0` static binary) · Go UI binary (`kern-ui`, talks to the core only via steering/observation) · Postgres (journal, budgets; pgvector later) · CI runs offline against kern-link's `faux` provider.

## Status

Design phase, July 2026. POC milestones: **M0** walking skeleton → **M1** harness → **M2** agents → **M3** supervision.

Conventions, design notes and package documentation live in the [wiki](https://github.com/kern-ia/kern-wiki). How to contribute: [CONTRIBUTING.md](https://github.com/kern-ia/.github/blob/main/CONTRIBUTING.md).
