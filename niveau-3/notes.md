# Niveau 3 — Synchronisation

## Ce que j'ai pratiquééé

### Simuler un travail à deux
- Modifié un fichier directement sur GitHub via l'interface web
- Fait un **Fetch** pour récupérer le commit distant sans toucher aux fichiers locaux
- `origin/main` se met à jour, `main` locale reste en place → indicateur `↓1`
- Fait un **Pull** pour fusionner le commit distant dans la branche locale

### Conflit local/distant avec pull --rebase
- Modifié la même ligne en local (commit non pushé) ET sur GitHub
- `git pull --rebase origin` rejoue le commit local *après* le commit distant au lieu de créer un merge commit
- En cas de conflit pendant le rebase, Git s'arrête et passe en HEAD détaché temporaire (état interne du rebase)
- Résolution : corriger le fichier, `git add`, puis `git rebase --continue`
- Résultat : historique linéaire sans merge commit

### Fetch avant Pull
- Bonne pratique : Fetch d'abord pour voir ce qui arrive, Pull ensuite pour fusionner
- Fetch = télécharge sans modifier les fichiers locaux
- Pull = Fetch + merge (ou rebase avec `--rebase`)

### Stash
<!-- à compléter -->
