# Bugs git-manager identifiés

## ~~Bug 1~~ — Faux avertissement push --force lors d'un amend ✓ Corrigé

**Symptôme :** lors d'un amend, git-manager affiche "Ce commit a déjà été pushé sur le remote. Un git push --force sera nécessaire pour l'écraser. Continuer quand même ?" même quand aucun remote n'est configuré.

**Contexte :** dépôt sans remote (`git remote -v` retourne vide). Premier amend après un commit local.

**Impact :** faux positif inquiétant pour l'utilisateur, mais sans conséquence — cliquer "Continuer quand même" fonctionne correctement.

**Comportement attendu :** l'avertissement ne devrait s'afficher que si un remote existe et que le commit a été pushé.

---

## ~~Bug 2~~ — Noms de branche avec slash refusés ✓ Corrigé

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

---

## ~~Bug 3~~ — Branche distante affichée comme `origin` au lieu de `origin/main` ✓ Corrigé

**Symptôme :** dans la section **Branches distantes**, git-manager affiche `origin` au lieu de `origin/main`. Le nom du remote est affiché à la place du nom complet de la branche distante.

**Impact :** trompeur — l'utilisateur croit que la branche s'appelle `origin` alors que c'est le nom du remote. La branche s'appelle `main` des deux côtés, seul le préfixe `origin/` indique qu'elle est distante.

**Comportement attendu :** afficher `origin/main` pour que le lien avec la branche locale `main` soit évident.

**Cas supplémentaire :** après suppression et remise du remote (`git remote remove origin` puis `git remote add origin <url>`), git-manager affiche deux entrées dans les branches distantes : `origin` (le nom du remote — Bug 3) ET `origin/main` (la vraie branche de suivi créée après le Fetch automatique). Avant la suppression, seul `origin` apparaissait.

---

## Amélioration UX 3 — Afficher le nom du remote dans l'interface

**Symptôme :** l'interface affiche l'URL du remote mais pas son nom (`origin`). Pour vérifier le nom, l'utilisateur doit passer par `git remote -v` en ligne de commande.

**Comportement attendu :** afficher le nom du remote (`origin`) à côté de l'URL dans la section de gestion du remote.

---

## Amélioration UX 4 — Distinguer HEAD détaché volontaire et HEAD détaché pendant un rebase

**Symptôme :** git-manager affiche le même message "HEAD détaché" que ce soit lors d'une exploration volontaire d'un ancien commit ou lors d'un `git rebase --continue` (où Git détache temporairement le HEAD en interne).

**Impact :** confusion — l'utilisateur croit être en HEAD détaché accidentellement alors que c'est un état normal et temporaire du rebase.

**Comportement attendu :** détecter si un rebase est en cours (présence de `.git/rebase-merge` ou `.git/rebase-apply`) et afficher un message distinct : "Rebase en cours — HEAD temporairement détaché" au lieu du message habituel.

---

## Amélioration UX 5 — Bouton "Continuer le rebase" dans l'interface

**Symptôme :** quand un rebase est interrompu par un conflit, l'utilisateur doit passer par la ligne de commande pour exécuter `git rebase --continue` (ou `git rebase --abort`).

**Comportement attendu :** détecter la présence de `.git/rebase-merge` ou `.git/rebase-apply` et afficher deux boutons dans l'interface :
- **Continuer le rebase** → `git rebase --continue` (une fois le conflit résolu et le fichier stagé)
- **Abandonner le rebase** → `git rebase --abort` (pour revenir à l'état avant le rebase)

Cette amélioration est liée à [[ux4-head-detache-rebase]] — les deux peuvent être implémentées ensemble.
