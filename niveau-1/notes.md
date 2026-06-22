# Niveau 1 — Les bases

## Ce que j'ai pratiqué

### Premier commit
- Créé le dépôt SandBox-git-manager
- Stagé CLAUDE.md et .gitignore (`git add`)
- Fait le premier commit : `Initial commit` (hash : d21c8ce)
- Statut avant staging : `??` (Untracked)
- Statut après staging : `A` (Added)

### Statuts Git à retenir
| Statut | Signification |
|--------|---------------|
| `??`   | Fichier non suivi (Untracked) |
| `A`    | Ajouté en staging (Added) |
| `M`    | Modifié (Modified) |
| `D`    | Supprimé (Deleted) |
| `U`    | Conflit non résolu (Unmerged) |

### Zone de staging
La zone de staging (index) est une étape intermédiaire entre le dossier de travail et le commit.
- `git add` → déplace les changements vers le staging
- `git commit` → enregistre le staging dans l'historique

## Exercice en cours
Je modifie ce fichier pour observer le statut M (Modified) dans git-manager.

