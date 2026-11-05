# Analyse indépendante — Agent 3 : UX / Designer d'interface

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait · 🟨 Hypothèse · 🟩 Recommandation

## 1. Problème métier

🟦 Les erreurs viennent d'un flux oral et papier. Côté interface, cela se traduit par : saisie lente, lisibilité faible, pas de retour visuel sur l'état d'une commande.

## 2. Acteurs (vue expérience)

🟦 4 acteurs, mais **3 contextes d'usage très différents** :
- 🟨 Serveur : en salle, en mouvement, parfois avec les mains occupées → saisie rapide, grands boutons.
- 🟨 Cuisinier : en cuisine (chaleur, graisse, bruit) → écran « glanceable », contraste élevé, statut visible de loin.
- 🟨 Caissier : au comptoir, opération financière → clarté absolue des montants, confirmation explicite.
- 🟨 Gérant : au bureau, analyse → graphiques et filtres de période.

## 3. Fonctionnalités (traduction UX)

🟩 Carte de la salle (tables avec état coloré) comme écran d'accueil serveur.
🟩 Écran cuisine : file de commandes triée par ancienneté, un geste pour changer de statut.
🟩 Facture : récapitulatif lisible + saisie du montant reçu + rendu affiché en grand.

## 4. Interactions

🟦 Le serveur doit **voir en temps réel** que la cuisine a bien reçu et où en est sa commande — c'est le cœur de la confiance dans l'outil.

## 5. Contraintes

🟦 Hors scope V1 : paiement en ligne (donc pas d parcours de paiement complexe), pas de fidélité.
🟨 Hypothèse : le personnel a un rapport hétérogène au numérique → l'appli doit être utilisable après une formation très courte.

## 6. Risques

🟩 **Adoption** : si la saisie d'une commande prend plus de temps que le papier, l'outil sera contourné. C'est le risque n°1 côté UX.
🟩 Lisibilité de l'écran cuisine dans un environnement difficile.
🟩 Erreur de saisie (mauvais plat, mauvaise quantité) → prévoir une correction simple avant envoi.

## 7. Questions client

1. Quels appareils seront réellement utilisés (tablettes, PC de caisse, écran cuisine dédié) et quelles tailles d'écran ?
2. Niveau de confort numérique de l'équipe (formation nécessaire ?) ?
3. La cuisine est-elle proche de la caisse ou séparée (visibilité des écrans) ?
4. Faut-il des photos des plats dans l'appli ?
5. Langue de l'interface : français confirmé, mais y a-t-il des termes métier locaux à respecter ?
