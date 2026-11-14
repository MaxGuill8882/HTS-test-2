# Le Carnet de la Maison

Une application web statique (HTML + JavaScript) pour gérer les tâches quotidiennes de la maison par personne (parents / enfants). Les tâches sont définies par personne dans des fichiers JSON côté dépôt, l'état se synchronise en temps réel via Firestore, les enfants s'identifient avec un PIN et les parents peuvent valider/dévalider les tâches. Un envoi d'e‑mail est déclenché lors de la complétion des tâches (EmailJS). Les photos de profil peuvent être stockées dans Firebase Storage (optionnellement — le dépôt contient aussi une intégration pour pousser des images vers GitHub depuis le client, mais cela comporte des risques de sécurité).

## Fonctionnalités principales
- Sélection d'un utilisateur (carte) puis identification par PIN.
- Affichage des tâches par jour (fichiers config/<id>.json).
- Marquer une tâche comme terminée (confirmation modal).
- Parents : possibilité de valider ou décocher une tâche.
- Notifications par e‑mail via EmailJS (file d'attente pour respecter les limites).
- Thèmes colorés personnalisables par utilisateur (sauvegardés dans Firestore).
- Avatar/photo de profil stockée dans Firebase Storage.
- Synchronisation en temps réel des états via Firestore (doc : `carnet_maison/etat_taches`).

## Stack technique
- Langage : HTML + JavaScript (vanilla)
- Backend temps réel & stockage images : Firebase Firestore & Firebase Storage
- Envoi d'e‑mails côté client : EmailJS
- Déploiement : site statique (ex. GitHub Pages, tout serveur static)

## Contenu du dépôt (éléments importants)
- index.html — toute l'application (JS, CSS et logique).
- config/ — fichiers JSON par personne (ex. `maxime.json`, `yannick.json`, …).
  - Personnes actuelles : martin, laurence, maxime, yannick, myriam, valerie
- README.md — (ce fichier)

## Format d'un fichier config
Chaque personne a son fichier `config/<id>.json`. Exemple minimal :

```json
{
  "nom": "Maxime",
  "type": "enfant",        // "parent" ou "enfant"
  "pin": "****",          // code PIN à 4 chiffres
  "taches": {
    "lundi": ["Faire sa Chambre","Vider la litière cage (Soir)"],
    "mardi": [...],
    ...
  }
}
