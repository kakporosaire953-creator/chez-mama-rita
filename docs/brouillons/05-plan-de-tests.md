# 05 — Plan de tests et stratégie qualité

**Projet :** Chez Mama Rita
**Date :** 2026-11-04
**Statut :** Brouillon à valider

## 1. Objectifs qualité

- Zéro erreur de calcul sur les factures (calcul 100 % automatique, montants entiers XOF).
- Transmission des commandes à la cuisine en moins de 3 secondes.
- Aucune perte de commande, même en cas de coupure réseau local ou de coupure Internet.
- Application utilisable par chaque profil après ≤ 15 minutes de formation.

## 2. Niveaux de test

| Niveau | Quoi | Qui | Outil |
|--------|------|-----|-------|
| **Tests unitaires** | Fonctions isolées (calculs de facture, calcul du rendu, transitions de statut, règles métier) | Dev Back / Front | Jest / Vitest (JS) ou pytest (Python) |
| **Tests d'intégration / API** | Routes API, accès base de données, WebSocket | Dev Back + QA | Postman/Newman ou tests automatisés (Supertest) |
| **Tests E2E** | Scénarios complets dans le navigateur (commande table → cuisine → paiement) | QA | Playwright ou Cypress |
| **Tests de recette (UAT)** | Scénarios réels avec le client au restaurant | PO + QA + utilisateurs | Checklist signée |
| **Tests de charge / robustesse** | 10+ serveurs simultanés, coupure réseau, redémarrage serveur | QA + DevOps | Scripts de charge simples, scénarios manuels |

Couverture visée : ≥ 80 % sur le code métier critique (commandes, paiements, statuts).

## 3. Cas de test principaux (par exigence)

### 3.1 Menu (EF-01 à EF-05)
- [ ] Créer un plat → visible côté serveur immédiatement.
- [ ] Modifier un prix → les **nouvelles** commandes prennent le nouveau prix, les anciennes gardent l'ancien.
- [ ] Marquer un plat indisponible → non sélectionnable, grisé.
- [ ] Plat indisponible déjà dans une commande en cours → la ligne reste valide.

### 3.2 Commandes et statuts (EF-08 à EF-17)
- [ ] Créer une commande sur une table → horodatée, rattachée au serveur connecté.
- [ ] Envoyer en cuisine → apparaît sur l'écran cuisine en < 3 s (mesuré).
- [ ] Ajouter une ligne après envoi → notifiée en cuisine.
- [ ] Transition complète : en attente → en préparation → prêt → servi → payée, horodatages vérifiés.
- [ ] Deux serveurs commandent en même temps sur des tables différentes → aucune perte ni conflit.
- [ ] Annulation d'une commande non encore en préparation → motif obligatoire, trace dans le journal.
- [ ] Annulation d'une commande **déjà en préparation** → refusée (règle métier).
- [ ] Coupure du Wi-Fi du poste cuisine 30 s → à la reconnexion, l'écran cuisine retrouve l'état exact.

### 3.3 Facturation et paiements (EF-18 à EF-22)
- [ ] Facture de 3 plats × quantités variées → total exact (ex : 3500 + 2×5000 + 7000 = 20 500 XOF).
- [ ] Encaissement : reçu 25 000 pour une facture de 20 500 → rendu = 4 500 XOF.
- [ ] Montant reçu insuffisant → encaissement refusé, message clair.
- [ ] Numéro de facture unique et séquentiel ; facture consultable et réimprimable.
- [ ] Paiement d'une commande non servie → refusé (règle métier).
- [ ] Après paiement → table repasse « libre », commande marquée « payée ».
- [ ] 100 factures générées en boucle (test automatisé) → zéro erreur de calcul.

### 3.4 Tableau de bord (EF-23 à EF-26)
- [ ] CA du jour = somme réelle des factures du jour (vérifié sur un échantillon).
- [ ] Top plats = classement correct sur une période connue (jeu de données de test).
- [ ] Période personnalisée (ex : 01/10–15/10) → montants corrects.

### 3.5 Sécurité et rôles (EF-27 à EF-29)
- [ ] Un serveur ne peut pas accéder aux routes menu en écriture, caisse encaissement, dashboard, utilisateurs.
- [ ] Un cuisinier ne peut que changer les statuts des lignes.
- [ ] Mot de passe stocké haché en base (vérification technique).
- [ ] Compte désactivé → connexion impossible.
- [ ] Journal : annulation et encaissement tracés avec utilisateur et heure.

### 3.6 Non fonctionnelles
- [ ] Application fonctionnelle avec Internet du restaurant coupé (ENF-01).
- [ ] Sauvegarde manuelle → suppression de données de test → restauration → données retrouvées (ENF-06).
- [ ] Affichage correct sur tablette 10" et écran cuisine (ENF-04).

## 4. Environnements

| Environnement | Usage |
|---------------|-------|
| **Local (dev)** | Développement + tests unitaires/automatisés en continu |
| **Pré-production (mini-PC de test)** | Tests E2E, charge, recette interne |
| **Production (restaurant)** | Recette finale avec les vrais utilisateurs, puis mise en service |

## 5. Gestion des défauts

- Gravité : **Bloquant** (paiement/commande impossible), **Majeur** (fonction contournable), **Mineur** (cosmétique).
- Règle : aucun défaut Bloquant ouvert en production ; aucun Majeur ouvert en recette finale.
- Chaque bug est reproductible (étapes + capture) et tracé jusqu'à sa correction vérifiée.

## 6. Critères d'acceptation de la recette finale (à signer par le gérant)

1. Scénario complet du jour réel exécuté de bout en bout (commande → cuisine → service → encaissement → facture).
2. Tous les cas de test 3.1–3.6 exécutés, résultats consignés.
3. Formation des 4 profils réalisée ; chaque utilisateur autonome sur son périmètre.
4. Sauvegarde + restauration démontrées.
5. Guide utilisateur et procédure de sauvegarde remis.

---

*Plan de tests à valider avec le client. Les cas de test détaillés seront ensuite formalisés en fiches de test exécutables (document vivant pendant les sprints).*
