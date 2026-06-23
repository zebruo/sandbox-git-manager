# Niveau 1 — Exercices

## Exercice : Premier commit

**Objectif** : créer le tout premier commit d'un dépôt.

**Étapes :**
1. Ouvrir git-manager et sélectionner le dépôt
2. Dans la zone de staging, repérer les fichiers en statut `??` (Untracked)
3. Cocher `CLAUDE.md` et `.gitignore`
4. Écrire le message : `Initial commit`
5. Valider le commit

**Ce qu'on observe :**
- Statut avant staging : `??` (Untracked)
- Statut après staging : `A` (Added)
- `root-commit` dans la sortie → premier commit du dépôt, sans parent
- Le hash (ex: `d21c8ce`) identifie ce commit de façon unique

---

## Exercice : Modifier un fichier et observer les statuts A et M

**Objectif** : comprendre la zone de staging en observant les statuts en temps réel.

**Étapes :**
1. Créer un nouveau fichier (ex: `niveau-1/notes.md`)
2. Observer son statut dans git-manager : `??` (Untracked)
3. Le stager (`git add` ou bouton Stager) → statut passe à `A`
4. Modifier le fichier sans le re-stager
5. Observer : le fichier apparaît en `A` (staging) ET en `M` (working tree) simultanément
6. Re-stager pour inclure les dernières modifications
7. Commiter : `feat: add niveau-1 notes`

**Ce qu'on observe :**
- `??` → fichier inconnu de Git
- `A` → version stagée, prête pour le commit
- `M` → modification sur le disque, pas encore stagée
- Si on commite avec A+M, seule la version A part dans le commit

---

## Exercice : Lire un diff

**Objectif** : comprendre ce que Git affiche quand un fichier est modifié.

**Étapes :**
1. Modifier un fichier déjà commité (ajouter ou supprimer quelques lignes)
2. Dans git-manager, repérer le fichier en statut `M`
3. Cliquer sur son nom pour ouvrir la vue diff
4. Lire le diff et identifier :
   - L'en-tête `@@ -x,y +x,y @@` → numéro de ligne et nombre de lignes dans l'ancien/nouveau fichier
   - Les lignes `+` en vert → lignes ajoutées
   - Les lignes `-` en rouge → lignes supprimées
   - Les lignes sans signe → contexte inchangé

**Ce qu'on observe :**
```
@@ -26,3 +26,11 @@
```
→ bloc à partir de la ligne 26 ; 3 lignes avant, 11 après (8 lignes ajoutées)

---

## Exercice : Zone de staging — statuts A et M simultanés

**Objectif** : comprendre que Git suit le staging et le working tree séparément.

**Étapes :**
1. Modifier un fichier et le stager (bouton Stager ou `git add`)
2. Modifier à nouveau le même fichier sans le re-stager
3. Observer dans git-manager : le fichier apparaît en `A` ET en `M` simultanément
4. Comprendre que si on commite maintenant, seule la version `A` (stagée) est incluse
5. Pour inclure les dernières modifications : re-stager le fichier

---

## Exercice : Amend — corriger le dernier commit

**Objectif** : corriger un message oublié ou ajouter un fichier oublié dans le dernier commit.

**Étapes — corriger le message :**
1. Faire un commit avec un message volontairement mauvais (ex: `fix: notes`)
2. Dans git-manager, charger le message via le crayon ✏️ dans l'historique
3. Corriger le message dans le champ
4. Cliquer **Amend** (sans rien cocher)
5. Vérifier dans l'historique que le message a changé (et que le hash a changé)

**Étapes — ajouter un fichier oublié :**
1. Faire un commit en oubliant volontairement un fichier
2. Ne pas toucher au champ message
3. Cocher le fichier oublié dans la liste
4. Cliquer **Amend**
5. Vérifier que le fichier est maintenant dans le commit

**À retenir :** l'amend réécrit le commit (nouveau hash). Ne jamais amender un commit déjà pushé sur une branche partagée.

---

## Messages de commit utilisés

Convention : `type: description courte` (format Conventional Commits)

| Message | Type | Contexte |
|---------|------|----------|
| `Initial commit` | — | Premier commit du dépôt, convention universelle |
| `feat: add niveau-1 notes` | `feat` | Ajout d'un nouveau fichier de notes |
| `fix: notes` | `fix` | Message volontairement mauvais pour l'exercice amend |
| `docs: add diff visuel section` | `docs` | Message corrigé via amend — ajout de documentation |

**Types courants :**
- `feat` → nouvelle fonctionnalité ou nouveau contenu
- `fix` → correction d'un bug ou d'une erreur
- `docs` → modification de documentation uniquement
- `refactor` → réécriture sans changement de comportement
- `chore` → tâche technique (config, dépendances, gitignore)
