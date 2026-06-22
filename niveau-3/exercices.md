# Niveau 3 — Exercices

## Exercice : Simuler un travail à deux

**Objectif** : comprendre comment récupérer des modifications faites par quelqu'un d'autre (ou depuis GitHub directement).

**Étapes :**
1. Sur GitHub, ouvrir un fichier et le modifier via l'interface web → commiter
2. En local, faire un **Fetch** → observer `↓1` sur la branche locale
3. Faire un **Pull** → le commit distant arrive en local

**Ce qu'on observe :**
- Fetch met à jour `origin/main` sans toucher à `main` locale
- Pull fusionne `origin/main` dans `main` locale

---

## Exercice : Conflit local/distant avec pull --rebase

**Objectif** : comprendre la différence entre pull --rebase et pull classique, et résoudre un conflit de synchronisation.

**Étapes :**
1. Modifier une ligne d'un fichier en local → commiter (sans pusher)
2. Modifier la **même ligne** directement sur GitHub → commiter
3. En local, faire `git pull --rebase origin` → conflit
4. Ouvrir le fichier conflictuel, résoudre, supprimer les marqueurs, sauvegarder
5. `git add <fichier>`
6. `git rebase --continue`
7. `git push`

**Ce qu'on observe :**
- Pendant le rebase, Git passe en HEAD détaché temporairement — c'est normal
- Le résultat est un historique **linéaire** (pas de merge commit)
- Différence avec pull classique :
  - `pull` (merge) → crée un commit de fusion avec deux parents
  - `pull --rebase` → rejoue le commit local après le commit distant, pas de merge commit

**Piège :** git-manager affiche "HEAD détaché" pendant le rebase — ne pas confondre avec un HEAD détaché volontaire (exploration d'un ancien commit).

---

## Exercice : Stash

<!-- à compléter -->
