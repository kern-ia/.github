## Summary

<!-- What does this PR do, in one or two sentences? -->

## Linked issue / RFC

<!-- Closes #... — features and cross-package changes need an agreed issue or RFC first. -->

## Semver impact

<!-- Pick one: patch / minor / major / none — see .github repo, docs/versioning.md -->

## Checklist

- [ ] `gofmt` and `go vet` clean; build passes with `CGO_ENABLED=0`
- [ ] Tests pass **offline** (no live provider calls; `faux` provider for the LLM boundary)
- [ ] No personal data, verbatim provider payloads, or credentials in code, fixtures, or logs
- [ ] Stays inside this package's domain (brick test holds)
- [ ] Docs updated where behavior changed
