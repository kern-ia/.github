# The brick test

The core is a composition root over independent packages ("bricks"). Before a new package repo is created, the proposal must pass every point below. This is a gate, not a guideline.

## Checklist

1. **The core runs without it.** Absence degrades a capability; it never breaks the core.
2. **It owns exactly one domain.** If the description needs "and", it is two packages.
3. **Plugging it in upgrades the core without modifying any other package.** Integration happens in the composition root and via the norm — never by editing siblings.
4. **Untrusted execution stays out-of-process.** If the package runs code it does not own (skills, tools, external agents), that code runs in a capability-sandboxed subprocess, never in `osd`'s process.
5. **It lives in its own repo with its own semver.** Releases are independent; the core pins versions (see [versioning](versioning.md)).
6. **It is consumed only via the norm.** Manifests and declared interfaces are the contract; reaching into core internals — or another brick's internals — fails the test.

## Process

1. Open an **RFC issue** (the org-wide template embeds this checklist) answering all six points, plus: position relative to the hot path (`policies-gate → orchestration → guard → pii → kern-link → provider`), inline-blocking vs async-scoring, and privacy implications.
2. Discussion on the RFC until the design and the name (per the [naming convention](naming.md)) are agreed.
3. Repo is created; the RFC is linked from its initial README.

## Reference brick

[kern-link](https://github.com/julienlegoux/kern-proxy) is the template: it predates the core, owns one domain (the provider boundary), is consumed as a versioned dependency, and the core composes it without kern-link knowing anything about the core.
