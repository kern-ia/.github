# Versioning and releases

Every package repo is independently versioned with [semver](https://semver.org). The core composes bricks by **pinning exact versions** in its `go.mod`; nothing floats.

## Rules

- Tags are `vX.Y.Z`, annotated, on the default branch.
- **Pre-1.0 semantics:** while a package is `0.x`, a **minor** bump (`0.3.0` → `0.4.0`) may break; a **patch** bump must not. Consumers should expect churn until `1.0.0`.
- From `1.0.0` on, standard semver applies strictly: breaking → major, additive → minor, fix → patch.
- Go modules at major version ≥ 2 carry the `/vN` path suffix (`github.com/project-kern/kern-link/v2`) per the Go modules convention.
- Every PR declares its semver impact (patch / minor / major / none) in the PR template; the next tag is the max of the impacts merged since the last one.

## Changelog

Each release documents what changed: either a `CHANGELOG.md` (Keep a Changelog style) or a substantive annotated-tag / GitHub-release message. "Misc fixes" is not a changelog.

## Compatibility surface

A package's public API is: its exported Go identifiers **and** its manifest/norm contract. A change to either is a semver event. Internal packages (`internal/`) are free to churn.

## Deferred

Shared release automation (tagging workflows, goreleaser config) is deferred along with shared CI — see the [decision log](decisions.md).
