# CONVENTIONS.md — .github (org meta-repo)

Ce repo est la source des fichiers santé communautaire par défaut de l'organisation
(`CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, templates d'issues et de PR) : tout
repo `kern-ia` qui ne fournit pas sa propre version hérite de celle-ci. Il porte donc une
responsabilité particulière — une modification ici affecte silencieusement tous les autres
repos qui n'ont pas de fichier local équivalent.

## Branches

- `main` : branche stable. Protégée — aucun push direct.
- Branches de travail : `docs/<slug>`, `chore/<slug>`.
- Toute modification passe par une Pull Request, y compris pour ce repo — particulièrement
  ici, puisqu'un changement mal relu se propage à toute l'organisation.

## Commits

Conventional Commits : `docs:` pour le contenu, `chore:` pour la structure/templates.

## Pull Requests

- Un seul sujet par PR.
- Toute modification de `CONTRIBUTING.md`, `SECURITY.md` ou des templates doit lister
  explicitement, dans la description de la PR, les repos qui héritent du défaut modifié (donc
  qui n'ont pas de version locale) — pour rendre visible l'effet de bord organisationnel.

## Contenu à maintenir en cohérence

- `CONTRIBUTING.md` affirme que « chaque repo porte son propre `CONVENTIONS.md` » — c'est
  désormais vrai pour les 6 repos de l'org (voir le rapport d'audit livré avec cette PR). À
  garder vrai pour tout nouveau repo créé (ajouter la case correspondante à la checklist de
  création de repo si elle existe).
- `CONTRIBUTING.md` affirme aussi qu'« il n'y a pas de `CHANGELOG.md` », notes de version dans
  le tag annoté. `kern-link` déroge à cette règle avec un `CHANGELOG.md` réel et maintenu.
  À trancher explicitement : soit documenter `kern-link` comme exception assumée dans ce
  fichier, soit généraliser le `CHANGELOG.md` aux autres repos et retirer l'affirmation
  actuelle qui est aujourd'hui fausse en pratique.
- Le template PR (`.github/PULL_REQUEST_TEMPLATE.md`) renvoie vers le `CONVENTIONS.md` du
  repo pour tout ce que la CI ne peut pas vérifier elle-même — cohérent avec l'existence de
  ces fichiers, à ne pas casser en le modifiant.

## Sécurité / confidentialité

Ce repo définit `SECURITY.md` pour toute l'organisation — toute modification de la procédure
de signalement doit rester compatible avec le GitHub private vulnerability reporting déjà
activé sur chaque repo.
