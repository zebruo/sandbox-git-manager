# SandBox-git-manager AAAAAAAA

Dépôt d'entraînement à Git et à git-manager (interface web de gestion Git — stack PHP/JS vanilla, pas de framework).

## Contexte

git-manager est une interface web qui permet de gérer un dépôt Git sans ligne de commande. Ce repo SandBox sert à pratiquer les fonctionnalités de git-manager et à progresser sur Git/GitHub.

Le projet git-manager est dans le dossier voisin. Les deux sont accessibles depuis le sélecteur de dépôt multi-dépôts de git-manager (reposRoot configuré dans git-config.php).

## Plan d'entraînement

### Niveau 1 — Les bases
- Créer un repo vide, faire un premier commit, pousser sur GitHub
- Modifier un fichier, observer le statut M/A/D/U, comprendre la zone de staging
- Lire un diff visuel ligne par ligne
- Amender un commit (message oublié, fichier oublié)

### Niveau 2 — Branches
- Créer une branche feature, y faire des commits, fusionner sur main
- Renommer, supprimer une branche locale et distante
- Provoquer un conflit volontairement (modifier le même fichier sur deux branches) et le résoudre
- Explorer le HEAD détaché — se placer sur un ancien commit, créer une branche depuis cet état

### Niveau 3 — Synchronisation
- Simuler un travail à deux (modifier le repo directement sur GitHub puis puller)
- Provoquer un conflit entre local et distant, résoudre avec pull --rebase vs merge
- Utiliser le stash pour interrompre un travail en cours, changer de branche, reprendre

### Niveau 4 — Historique & récupération
- Revert d'un commit : comprendre qu'un revert crée un nouveau commit
- Récupérer un fichier depuis un commit précis
- Utiliser l'historique par fichier pour retrouver une version spécifique

### Niveau 5 — Avancé
- Créer des tags annotés, pousser une release sur GitHub
- Travailler avec plusieurs branches simultanées (hotfix + feature en parallèle)
- Utiliser le mode multi-dépôts pour gérer plusieurs projets depuis une seule interface

## Organisation suggérée

Chaque niveau peut correspondre à un dossier de fichiers markdown. Les fichiers servent à la fois de support d'exercice et d'historique de ce qui a été pratiqué.
