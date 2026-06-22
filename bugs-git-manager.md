# Bugs git-manager identifiés

## Bug 1 — Faux avertissement push --force lors d'un amend

**Symptôme :** lors d'un amend, git-manager affiche "Ce commit a déjà été pushé sur le remote. Un git push --force sera nécessaire pour l'écraser. Continuer quand même ?" même quand aucun remote n'est configuré.

**Contexte :** dépôt sans remote (`git remote -v` retourne vide). Premier amend après un commit local.

**Impact :** faux positif inquiétant pour l'utilisateur, mais sans conséquence — cliquer "Continuer quand même" fonctionne correctement.

**Comportement attendu :** l'avertissement ne devrait s'afficher que si un remote existe et que le commit a été pushé.

---

## Bug 2 — Noms de branche avec slash refusés

**Symptôme :** git-manager rejette les noms de branche contenant `/` avec le message "Nom de branche invalide. Utilisez uniquement lettres, chiffres, tirets, underscores et points."

**Exemple :** `feature/niveau-2` → refusé.

**Impact :** la convention `type/nom` (ex: `feature/`, `hotfix/`, `release/`) est très répandue et supportée nativement par Git. git-manager la bloque.

**Contournement :** utiliser un tiret à la place du slash (`feature-niveau-2`).

---

## Amélioration UX 1 — Fichier en double pendant la résolution de conflit

**Symptôme :** lors d'un conflit de fusion, le fichier concerné apparaît deux fois en `M` (Modified) dans la liste des fichiers modifiés.

**Contexte :** comportement observé lors de la résolution d'un conflit sur `niveau-2/notes.md`.

**Impact :** déroutant — l'utilisateur ne sait pas lequel modifier ou stager en premier.

**Comportement attendu :** regrouper les deux occurrences en une seule entrée avec un indicateur visuel clair "Conflit à résoudre", puis passer à `M` une fois les marqueurs supprimés et le fichier sauvegardé.
