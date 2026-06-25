# Niveau 2 — Branches correction
## Ce que j'ai pratiqué

### Créer une branche MAIN
- Créé la branche `feature-niveau-2` depuis `main`
- Basculé dessus avec `git checkout -b feature-niveau-2`
- git-manager n'accepte pas les slashes dans les noms de branche → utiliser des tirets

### Fusionner (Merge)
- Fusionné `feature-niveau-2` dans `main` → résultat : **Fast-forward**
- Fast-forward = `main` n'avait pas bougé pendant le travail sur la branche, Git avance simplement le pointeur sans créer de commit de fusion
- Merge commit = les deux branches ont divergé, Git crée un commit avec deux parents (visible dans l'historique avec `Merge: hash1 hash2`)

### Supprimer une branche
- Supprimé `feature-niveau-2` avec `git branch -d feature-niveau-2`
- Le `-d` (delete safe) vérifie que la branche est bien fusionnée avant de supprimer

### Conflit de fusion
- Provoqué un conflit en modifiant la même ligne sur `main` et `conflit-test`
- Git insère des marqueurs dans le fichier :
  ```
  <<<<<<< HEAD
  # Titre (version main)
  =======
  # Titre (version conflit-test)
  >>>>>>> conflit-test
  ```
- Résolution : choisir une version, supprimer les marqueurs, sauvegarder, stager, commiter
- Le commit de résolution est un **merge commit** (deux parents)
- Piège : pour obtenir un conflit, les deux branches doivent avoir divergé depuis un même point — commit sur `conflit-test` d'abord, puis commit sur `main`, puis merge

### HEAD détaché
- Se placer sur l'ancien commit `d21c8ce` (Initial commit) avec `git checkout d21c8ce`
- En HEAD détaché : aucune branche active, les fichiers sont tels qu'au moment du commit visité
- `niveau-1/`, `niveau-2/` et `bugs-git-manager.md` avaient disparu — seulement `CLAUDE.md` et `.gitignore` présents
- Retour à la normale : `git checkout main`
- Depuis un HEAD détaché, on peut créer une branche avec **Créer une branche ici** pour transformer cet état en branche officielle
