# QUALPACK V27 START

Version de travail basée sur QUALPACK V26 TEST.

## Objectif V27 START

- Conserver la sécurité V26 : `site_id`, clé d’accès, RLS Supabase, licence/expiration.
- Ajouter un mini back-office ADMIN intégré.
- Réduire la dépendance au fichier Excel pour l’onboarding.
- Conserver l’import Excel comme Mode 2.

## Modifications principales

- Ajout du fichier `admin.js`.
- Déplacement dans `admin.js` de :
  - logique PIN Admin,
  - ouverture Admin,
  - import Excel,
  - prévisualisation import,
  - validation import,
  - rendu catalogue Admin,
  - gestion opérateurs,
  - synchronisation manuelle.
- Ajout du Mode rapide terrain V27 START dans l’écran Admin :
  - ajout client,
  - ajout ligne + détecteur par défaut,
  - ajout produit.
- Ajout de `admin.js` dans `app.html` après `sync.js`.
- Ajout de `admin.js` dans le cache PWA de `sw.js`.

## Supabase

Aucune modification de schéma Supabase n’est incluse dans ce ZIP.
Aucune policy RLS n’est modifiée.
V26 TEST peut continuer à utiliser les mêmes tables Supabase.

## Point important

Déployer cette version dans un dépôt ou dossier GitHub Pages séparé de V26 TEST, par exemple :

`QUALPACK-V27-START`

Cela permet aux sites pilotes Moulin des Moines, Traiteur de la Thur et codex_test de continuer leurs tests sur V26 TEST pendant que V27 START est testée séparément.

## Tests recommandés après déploiement

1. Ouvrir V27 START avec `?site_id=codex_test`.
2. Saisir la clé du site.
3. Ouvrir Admin avec le PIN.
4. Vérifier que l’import Excel fonctionne toujours.
5. Ajouter un client en Mode rapide terrain.
6. Ajouter une ligne + détecteur.
7. Ajouter un produit.
8. Vérifier que le produit apparaît dans la page Pesées.
9. Vérifier que V26 TEST fonctionne toujours sur son URL actuelle.

## Correctif UX V27 START

- Ajout des boutons **Retirer** dans les listes rapides (opérateurs, clients, lignes/détecteurs, produits).
- Les actions **Retirer** ne réalisent pas de suppression physique Supabase.
- Les produits et opérateurs sont désactivés (`actif = false`) quand la table le permet.
- Les clients et lignes sont masqués côté configuration rapide pour éviter les suppressions risquées.
- Correction du formulaire Ligne : l'identifiant est désormais laissé à Supabase lorsque la table utilise un id numérique.

## Révision UX — Mode START isolé

- Le badge `QUALPACK V27 START — Configuration rapide terrain` est conservé.
- Les mini-listes du Mode START affichent uniquement les éléments ajoutés via le Mode START sur le site/appareil courant.
- Elles ne reprennent pas automatiquement tout le catalogue V26 ou l'import Excel, pour éviter de surcharger l'expérience auditeur / petit site.
- Les actions restent sans DELETE physique Supabase :
  - `Retirer` pour les opérateurs,
  - `Supprimer` pour les lignes et produits, avec désactivation/masquage logique.
- Supabase, les tables et les policies RLS ne sont pas modifiées.


## Correction visibilité badge START

- Ajout d’un badge plus visible `MODE START` dans le bloc Mode rapide terrain.
- Le badge `QUALPACK V27 START — Configuration rapide terrain` reste présent et plus lisible.
- Aucun changement Supabase, aucune modification RLS, aucun DELETE physique.


## Correction UX Admin — bloc sécurité retiré

Le bloc supérieur « Sécurité / Code PIN d’accès » a été supprimé de l’écran Admin afin d’éviter la redondance avec la demande de PIN réalisée à l’entrée de l’Admin.

La fonction de réinitialisation du PIN reste disponible dans le bloc « Informations » en bas de page.

Cette modification est uniquement front-end dans QUALPACK V27 START et n’a aucune incidence sur Supabase ni sur QUALPACK V26 TEST.
