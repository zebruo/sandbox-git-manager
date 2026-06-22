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

---

## Amélioration UX 2 — Design de la div HEAD détaché

**Symptôme :** la bannière d'avertissement HEAD détaché occupe trop de place dans l'interface.

**Code concerné :** `git-manager.html`, bloc `if (isDetached)` dans la fonction de rendu des branches.

```js
if (isDetached) {
  html += `
    <div class="alert alert-info" style="margin-bottom: 15px;">
      <i class="fas fa-exclamation-triangle"></i>
      <strong>HEAD détaché</strong> sur le commit <code>${detachedAt}</code><br>
      <small>Vous n'êtes sur aucune branche. Basculez sur une branche ou créez-en une depuis ce commit.</small>
      <div style="margin-top: 10px;">
        <button class="btn btn-primary" onclick="createBranchFromDetached()" style="padding: 5px 12px; font-size: 0.85em;">
          <i class="fas fa-code-branch"></i> Créer une branche ici
        </button>
      </div>
    </div>
  `;
}
```

**Impact :** la div prend toute la largeur et pousse le reste du contenu vers le bas.

**Comportement attendu :** revoir le design pour qu'il soit plus compact — bannière fine ou inline, sans perturber la mise en page générale.
