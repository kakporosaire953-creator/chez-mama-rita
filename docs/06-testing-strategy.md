# 06 — Stratégie de tests

**Projet :** Chez Mama Rita
**Statut :** 🟡 **À analyser** — aucune stratégie validée
**Dernière mise à jour :** 2026-11-04

> Aucun cas de test définitif ne sera rédigé sur des exigences non validées.
> Aucun code de test n'est produit à ce stade.

## 1. Objectifs qualité (issus du brief)

🟦 Zéro erreur à la facturation (calcul automatique).
🟦 Coordination fiable entre salle, cuisine et caisse.

## 2. Niveaux de test envisagés — 🟡 À analyser

| Niveau | Description | Statut |
|--------|-------------|--------|
| Unitaires | Calculs (facture, rendu), règles métier | 🟡 À définir |
| Intégration / API | Routes, base de données, transmissions | 🟡 À définir |
| E2E | Scénarios complets navigateur (commande → paiement) | 🟡 À définir |
| Recette (UAT) | Avec le client au restaurant | 🟡 À définir (Q13) |
| Robustesse | Coupure réseau, redémarrage, utilisateurs simultanés | 🟡 À définir (Q14) |

## 3. Scénarios critiques identifiés (brouillon)

- Transmission commande → cuisine (fiabilité, délai).
- Changements de statuts horodatés et visibles.
- Calcul de facture et rendu de monnaie (ex. 25 000 − 20 500 = 4 500 XOF).
- Refus d'encaissement d'une commande non servie (règle dépend de Q2).
- Sauvegarde / restauration.

## 4. Environnements — 🔴 Non défini

## 5. Politique de défauts — 🟡 À définir

Gravités : Bloquant / Majeur / Mineur — règles à valider.

## 6. Références

- Brouillon détaillé : `docs/brouillons/05-plan-de-tests.md` (cas de test préliminaires).
- `docs/analyse/05-qa-testeur.md`.
- Voir aussi : `tests/README.md`.
