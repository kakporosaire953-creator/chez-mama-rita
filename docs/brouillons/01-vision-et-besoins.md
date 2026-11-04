# 01 — Vision du produit et expression du besoin

**Projet :** Chez Mama Rita — solution de gestion numérique
**Restaurant :** Chez Mama Rita, Cotonou, Bénin
**Date :** 2026-11-04
**Statut :** Brouillon à valider (étape 1 du processus — aucune ligne de code avant validation)

---

## 1. Contexte

Chez Mama Rita est un restaurant situé à Cotonou qui fonctionne encore entièrement au papier :
les serveurs prennent les commandes sur papier, les transmettent **oralement** à la cuisine, et la
facturation se fait manuellement. Ce mode de fonctionnement génère des erreurs (plats oubliés,
mauvais plats, erreurs de addition) et une mauvaise coordination entre la salle, la cuisine et la caisse.

## 2. Problèmes constatés

| # | Problème | Conséquence |
|---|----------|-------------|
| P1 | Commandes papier transmises oralement à la cuisine | Plats oubliés, erreurs de préparation, aucune traçabilité |
| P2 | Facturation manuelle | Erreurs de calcul, temps perdu, contestations clients |
| P3 | Aucun suivi de l'état des commandes | Les serveurs ne savent pas quand un plat est prêt |
| P4 | Pas de visibilité sur les ventes | Le gérant ne dispose d'aucune donnée pour décider (plats populaires, heures de pointe) |
| P5 | Gestion des disponibilités des plats inexistante | Un plat « fini » est encore vendu aux clients |

## 3. Objectifs du projet

1. **Fluidifier les opérations** du restaurant de la prise de commande jusqu'au paiement.
2. **Améliorer la coordination** entre la salle, la cuisine et la caisse grâce à une transmission automatique et en temps réel des commandes.
3. **Sécuriser la facturation** en automatisant le calcul des additions.
4. **Donner au gérant des tableaux de bord** fiables (ventes, plats les plus commandés).

## 4. Acteurs et leurs besoins

| Acteur | Besoin principal |
|--------|------------------|
| **Serveur** | Prendre la commande d'une table rapidement, voir l'état d'avancement de chaque plat, encaisser sans erreur |
| **Cuisinier** | Recevoir les commandes automatiquement, signaler quand un plat est prêt |
| **Caissier** | Générer et encaisser les factures, corriger une commande avant paiement |
| **Gérant** | Gérer le menu (plats, prix, disponibilités), consulter les ventes et les statistiques, gérer les comptes utilisateurs |

## 5. Périmètre

### ✅ Dans le périmètre (V1)

- Gestion des plats, prix et disponibilités (menu)
- Prise de commandes par table
- Transmission automatique des commandes à la cuisine (écran cuisine / KDS)
- Suivi des statuts des commandes (en attente → en préparation → prêt → servi → payé)
- Paiements et factures simples (espèces, avec rendu de monnaie)
- Tableau de bord des ventes et des plats les plus commandés

### ❌ Hors périmètre (explicitement exclus pour le moment)

- Paiement mobile en ligne (Mobile Money, carte bancaire en ligne)
- Gestion des stocks
- Programme de fidélité
- Gestion multi-restaurants

## 6. Hypothèses et contraintes

- **Langue de l'application :** français.
- **Devise :** franc CFA (XOF), montants entiers.
- **Matériel visé :** tablettes pour les serveurs, un écran en cuisine, un poste caisse — l'application doit être **responsive** (web).
- **Connectivité :** Internet peut être instable à Cotonou → l'application doit fonctionner sur un **serveur local** dans le restaurant (réseau local Wi-Fi), avec sauvegarde locale prioritaire.
- **Déploiement visé :** installation sur place (on-premise), sans dépendance à un hébergeur cloud obligatoire.

## 7. Critères de succès (mesurables)

- 100 % des commandes passent par l'application (plus de papier) après la période de transition.
- Temps moyen de saisie d'une commande table < 2 minutes.
- Zéro erreur de calcul sur les factures (calcul automatique).
- Le gérant consulte le tableau de bord au moins 1 fois par jour.
- Taux d'erreurs de préparation (plat non commandé / oublié) en baisse mesurable après 1 mois.

---

*Document à valider par le client (gérant de Chez Mama Rita) avant de passer à l'analyse détaillée des exigences.*
