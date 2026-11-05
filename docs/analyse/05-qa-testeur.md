# Analyse indépendante — Agent 5 : Responsable Qualité / Tests

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait · 🟨 Hypothèse · 🟩 Recommandation

## 1. Problème métier

🟦 Les erreurs de facturation sont le symptôme visible. Côté qualité, cela signifie : **le processus commande→paiement n'est pas vérifiable**. L'appli doit rendre chaque étape testable et traçable.

## 2. Acteurs (vue test)

🟦 4 rôles = 4 parcours à tester, plus les transitions de responsabilité entre eux (ex : la commande passe du serveur au cuisinier sans perte).

## 3. Fonctionnalités testables (critères dérivés du brief)

- 🟦 Transmission auto à la cuisine → critère : la commande apparaît côté cuisine sans action humaine, rapidement.
- 🟦 Suivi des statuts → critère : chaque changement est daté et visible des bons acteurs.
- 🟦 Paiements/factures → critère : **zéro erreur de calcul**, rendu de monnaie correct, facture numérotée.
- 🟦 Disponibilités → critère : un plat marqué indisponible ne peut plus être commandé.
- 🟦 Dashboard → critère : les totaux correspondent exactement à la somme des factures.

## 4. Interactions à tester

🟩 Scénario critique de bout en bout : table occupée → commande envoyée → cuisine prépare → prêt → servi → encaissement → facture → table libérée.
🟩 Scénarios de rupture : coupure réseau, redémarrage, deux utilisateurs simultanés sur la même table.

## 5. Contraintes

🟦 Pas de paiement en ligne en V1 → les tests de paiement se concentrent sur espèces + rendu + facture imprimée/PDF.

## 6. Risques qualité

🟩 Perte d'une commande entre la tablette et l'écran cuisine (silencieuse) → test de fiabilité de la transmission obligatoire.
🟩 Double saisie / double envoi (double clic) → à tester.
🟩 Données perdues après panne → test de sauvegarde/restauration.
🟩 Le tableau de bord affiche des chiffres faux → perte de confiance du gérant.

## 7. Questions client

1. Quel temps d'indisponibilité maximum est acceptable en service (ex : 5 min) ?
2. Qui exécute la recette et la signe côté client ?
3. Y a-t-il des exigences de conservation des données (durée légale des factures) ?
4. Faut-il un mode « formation » avec des données fictives pour entraîner l'équipe ?
