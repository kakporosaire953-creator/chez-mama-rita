# Analyse indépendante — Agent 6 : Sécurité & DevOps

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait · 🟨 Hypothèse · 🟩 Recommandation

## 1. Problème métier

🟦 Un système de caisse concentre des données financières et des comptes utilisateurs : il doit être **protégé et sauvegardé**, même en mono-site.

## 2. Acteurs (vue sécurité)

🟦 4 rôles → contrôle d'accès par rôle obligatoire. 🟩 Un serveur ne doit jamais pouvoir modifier un prix ou encaisser ; un cuisinier ne doit pas voir la caisse.

## 3. Exigences de sécurité dérivées

- 🟩 Mots de passe jamais en clair, sessions avec expiration (postes partagés en salle).
- 🟩 Journal des actions sensibles : encaissements, annulations, changements de prix.
- 🟩 Sauvegarde automatique quotidienne + restauration testée régulièrement.
- 🟨 Hypothèse : déploiement sur un poste local du restaurant → le poste serveur doit être physiquement protégé (comptoir, local fermé).

## 4. Contraintes

🟦 Mono-site, pas de paiement en ligne en V1 → la surface d'attaque externe est réduite, mais le risque interne (poste partagé, accès physique) domine.

## 5. Risques

🟩 Vol ou perte du poste serveur = perte de tout l'historique → sauvegarde externe (clé USB, second disque, NAS).
🟩 Connexion d'un compte depuis un appareil non prévu → limiter les sessions, déconnexion auto.
🟨 Hypothèse : obligations de protection des données personnelles au Bénin (données du personnel) → à confirmer avec le client.

## 6. Questions client

1. Qui administre les comptes (le gérant lui-même ?) et avec quelle procédure de départ d'un employé ?
2. Quel support de sauvegarde est disponible sur place (clé USB, disque externe, NAS) ?
3. Le poste serveur sera-t-il dans un endroit verrouillable ?
4. Faut-il restreindre l'accès à certaines heures (ex : la caisse verrouillée la nuit) ?
5. Y a-t-il des exigences légales béninoises de protection des données à respecter ?

## 7. Note

🟨 Toute proposition de déploiement (conteneurisation, etc.) reste une **proposition** à valider ; aucune décision technique définitive à ce stade.
