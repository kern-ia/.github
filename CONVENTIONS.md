# CONVENTIONS.md — .github (org meta-repo)

This repo is the source of the organization's default community-health files
(`CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, issue and PR templates): any
`kern-ia` repo that doesn't provide its own version inherits this one. It therefore carries a
particular responsibility — a change here silently affects every other repo that doesn't have
a matching local file.

## Language

Code and comments (any tooling or scripts added to this repo) are written in English — no
exceptions. Internal documentation such as this file stays in whatever language the team
works in day to day; the org-wide files this repo defines (`CONTRIBUTING.md`,
`CODE_OF_CONDUCT.md`, `SECURITY.md`, templates) are already in English and should stay that
way, since they're public-facing and inherited org-wide.

## Branches

- `main`: stable branch. Protected — no direct pushes.
- Working branches: `docs/<slug>`, `chore/<slug>`.
- Any change goes through a Pull Request, including on this repo — especially here, since a
  poorly reviewed change propagates to the whole organization.

## Commits

Conventional Commits: `docs:` for content, `chore:` for structure/templates.

## Pull Requests

- One subject per PR.
- Any change to `CONTRIBUTING.md`, `SECURITY.md`, or the templates must explicitly list, in
  the PR description, which repos inherit the modified default (i.e. which ones have no local
  version) — to make the organizational side effect visible.

## Content to keep consistent

- `CONTRIBUTING.md` states that "each repo carries its own `CONVENTIONS.md`" — now true for
  all 6 org repos (see the audit report shipped with this PR). Keep it true for any new repo
  created (add the matching item to the repo-creation checklist if one exists).
- `CONTRIBUTING.md` also states "there is no `CHANGELOG.md`," release notes living in the
  annotated tag. `kern-link` deviates from this rule with a real, maintained `CHANGELOG.md`.
  To decide explicitly: either document `kern-link` as an accepted exception in this file, or
  generalize `CHANGELOG.md` to the other repos and remove the current statement, which is
  false in practice today.
- The PR template (`.github/PULL_REQUEST_TEMPLATE.md`) points to the repo's `CONVENTIONS.md`
  for anything CI cannot verify on its own — consistent with these files existing now, do not
  break that link when editing it.

## Security / privacy

This repo defines `SECURITY.md` for the whole organization — any change to the reporting
procedure must stay compatible with GitHub private vulnerability reporting, already enabled
on every repo.
