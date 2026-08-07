# Versioning and releases

Every package repo is independently versioned with [semver](https://semver.org). The core composes bricks by **pinning exact versions** in its `go.mod`; nothing floats.

## Rules

- Tags are `vX.Y.Z`, annotated, on the default branch.
- **Pre-1.0 semantics:** while a package is `0.x`, a **minor** bump (`0.3.0` → `0.4.0`) may break; a **patch** bump must not. Consumers should expect churn until `1.0.0`.
- From `1.0.0` on, standard semver applies strictly: breaking → major, additive → minor, fix → patch.
- Go modules at major version ≥ 2 carry the `/vN` path suffix (`github.com/kern-ia/kern-link/v2`) per the Go modules convention.
- Every PR declares its semver impact (patch / minor / major / none) in the PR template; the next tag is the max of the impacts merged since the last one.

## Release notes

**No `CHANGELOG.md`.** Every repo documents itself as an OKF bundle, and the bundle's `log.md` already carries the history of what changed. A second hand-maintained history file duplicates that work and drifts from it within a release or two.

What `log.md` does not answer is *"what breaks if I move from `v0.4.0` to `v0.5.0`"* — its entries are grouped by date, not by tag. That is the **release note**: the annotated tag message, which GitHub surfaces as a Release. Every tag carries one, and it states:

- the semver impact and what drove it — the PR template collects this per-PR, the tag aggregates it;
- **what breaks, explicitly**, whenever a `0.x` minor bump breaks anything. Pre-1.0 this is the note's whole reason to exist;
- what a consumer has to change to adopt the version.

"Misc fixes" is not a release note.

## Compatibility surface

A package's public API is: its exported Go identifiers **and** its manifest/norm contract. A change to either is a semver event. Internal packages (`internal/`) are free to churn.

## Deferred

Shared release automation (tagging workflows, goreleaser config) is deferred along with shared CI — see the [decision log](decisions.md).
