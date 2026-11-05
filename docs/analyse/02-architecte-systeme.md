# Analyse indépendante — Agent 2 : Architecte Système

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait · 🟨 Hypothèse · 🟩 Recommandation

## 1. Problème métier

🟦 Chaîne commande → cuisine → caisse sans trace numérique. L'architecture doit rendre ce flux **fiable, traçable et observable en temps réel**.

## 2. Acteurs (vue système)

🟦 4 rôles humains. 🟩 Ils se traduisent en **4 profils d'accès** distincts : un même socle, des droits différents (RBAC). C'est une exigence d'architecture, pas un choix technique.

## 3. Fonctionnalités (impact architecture)

- 🟦 Transmission automatique à la cuisine + suivi des statuts → implique un mécanisme **push** (temps réel) entre serveur et écran cuisine. 🟩 Options à comparer en conception : WebSocket, SSE, polling fréquent. **Aucune décision prise ici.**
- 🟦 Paiements et factures → intégrité des données financières (transactions, montants figés à la commande).
- 🟦 Tableau de bord → données historiques conservées, requêtes d'agrégation.
- 🟦 Gestion des disponibilités → état mutable du menu, propagé immédiatement aux postes de saisie.

## 4. Interactions

🟦 Le point clé est la **commande** comme objet central partagé par 3 acteurs (serveur, cuisinier, caissier) avec des droits différents sur ses états.

## 5. Contraintes et limites

🟦 Mono-établissement → pas d'architecture distribuée multi-sites.
🟦 Pas de paiement en ligne → la caisse reste un encaissement local (espèces au minimum).
🟨 Hypothèse : connectivité Internet possiblement instable à Cotonou → privilégier un fonctionnement **autonome sur le réseau local**.
🟨 Hypothèse : le matériel existant est hétérogène (PC, tablettes ?) → une application web responsive couvre tous les écrans.

## 6. Risques

🟩 Concurrence : deux serveurs sur la même table en même temps → verrouillage/gestion de conflits à prévoir.
🟩 Perte de données (panne du poste serveur) → sauvegardes automatiques indispensables.
🟩 Latence cuisine : si la notification n'arrive pas, la cuisine ne sait pas qu'une commande existe → file d'attente persistée côté serveur.

## 7. Questions client

1. Volume estimé : combien de commandes par jour en pic ?
2. Combien d'appareils simultanés au maximum (serveurs + cuisine + caisse) ?
3. Y a-t-il déjà un réseau Wi-Fi fiable dans le restaurant ? Un poste fixe dédié ?
4. Faut-il conserver l'historique des commandes/factures, et combien de temps ?
5. Exigences légales béninoises sur les tickets de caisse / factures (mentions obligatoires, TVA) ?

## 8. Note sur le document 03

🟨 Le brouillon `docs/brouillons/03-architecture-et-donnees.md` contient des **propositions** technologiques (ex : PostgreSQL, PWA). Ce ne sont pas des faits ni des décisions : elles restent à valider en revue d'architecture. Une alternative plus légère (SQLite) devra être comparée.
