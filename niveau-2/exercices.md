# Niveau 2 — Exercices

## Exercice : Créer une branche, commiter, fusionner

**Objectif** : comprendre le cycle de vie d'une branche feature.

**Étapes :**
1. Créer une branche depuis `main` : `git checkout -b feature-nom`
2. Faire un ou plusieurs commits sur cette branche
3. Revenir sur `main` : `git checkout main`
4. Fusionner : `git merge feature-nom`
5. Supprimer la branche : `git branch -d feature-nom`

**Ce qu'on observe :**
- **Fast-forward** : si `main` n'a pas bougé pendant qu'on travaillait sur la branche, Git avance simplement le pointeur — pas de commit de fusion créé
- **Merge commit** : si les deux branches ont divergé, Git crée un commit avec deux parents

---

## Exercice : Provoquer et résoudre un conflit

**Objectif** : comprendre pourquoi un conflit se produit et comment le résoudre.

**Prérequis :** avoir un fichier commité sur `main` (ex: `niveau-2/notes.md`).

**Étapes — créer le conflit :**
1. S'assurer d'être sur `main`
2. Créer la branche `conflit-test` : `git checkout -b conflit-test`
3. Sur `conflit-test` : modifier la ligne 1 du fichier → `# Titre (version conflit-test)` → commiter
4. Revenir sur `main` : `git checkout main`
5. Sur `main` : modifier la **même ligne 1** → `# Titre (version main)` → commiter
6. Fusionner : `git merge conflit-test`

**Résultat attendu :**
```
CONFLICT (content): Merge conflict in niveau-2/notes.md
Automatic merge failed; fix conflicts and then commit the result.
```

**Étapes — résoudre le conflit :**
1. Ouvrir le fichier en conflit — Git a inséré des marqueurs :
```
<<<<<<< HEAD
# Titre (version main)
=======
# Titre (version conflit-test)
>>>>>>> conflit-test
```
2. Choisir quelle version garder (ou écrire une version combinée)
3. Supprimer les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`
4. Sauvegarder le fichier
5. Stager le fichier : `git add niveau-2/notes.md`
6. Commiter : `git commit -m "resolve: conflit titre notes"`

**Ce qu'on observe :**
- Le commit de résolution est un **merge commit** (deux parents visibles dans l'historique)
- Pendant la résolution, le fichier apparaît deux fois dans git-manager : `U` (conflit) et `M` (modifié après résolution) — c'est normal

**Nettoyage :**
```bash
git branch -d conflit-test
```

**Ordre clé à retenir :**
```
main        ──A──────B (version main)
                \
conflit-test     C (version conflit-test)
```
Pour un conflit, il faut que A soit le point de départ commun, et que B et C modifient la même ligne chacun de leur côté.

> **Piège fréquent :** commit sur `conflit-test` d'abord, puis commit sur `main`, puis merge — dans cet ordre. Si on ne commite pas sur `main` après avoir créé `conflit-test`, Git fait un fast-forward au lieu d'un conflit.

---

## Exercice : HEAD détaché

*(à compléter)*
