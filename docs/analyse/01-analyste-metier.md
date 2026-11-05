# Analyse indépendante — Agent 1 : Analyste Métier (BA)

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait (énoncé par le client) · 🟨 Hypothèse (à vérifier) · 🟩 Recommandation

## 1. Problème métier

🟦 Le restaurant fonctionne au papier : commandes prises sur papier, transmises **oralement** à la cuisine, facturation manuelle.
🟦 Conséquence avérée : des erreurs surviennent, notamment à la facturation.
🟩 Reformulation : le problème n'est pas « informatiser », c'est **fiabiliser la chaîne commande → cuisine → caisse → paiement**, qui aujourd'hui n'a aucune trace ni aucun contrôle.

## 2. Acteurs et responsabilités

🟦 Quatre acteurs : **Serveur, Cuisinier, Caissier, Gérant**.
🟩 Responsabilités déduites du flux métier (à confirmer avec le client) :
- Serveur : prend la commande de sa table, suit son avancement.
- Cuisinier : prépare ce qui lui est transmis, signale la disponibilité.
- Caissier : établit et encaisse la facture.
- Gérant : supervise, gère le menu et exploite les données de vente.

## 3. Fonctionnalités attendues

🟦 Liste du brief : gestion plats/prix/disponibilités ; commande par table ; transmission auto à la cuisine ; suivi des statuts ; paiements + factures simples ; tableau de bord ventes + plats populaires.
🟩 Chaque fonctionnalité répond à un problème métier identifié (voir doc 01 §2) : la correspondance problème ↔ fonctionnalité est bonne, le périmètre est cohérent.

## 4. Interactions entre acteurs

🟦 Flux implicite : Serveur → (commande) → Cuisinier → (plat prêt) → Serveur → (addition) → Caissier → (données) → Gérant.
🟨 Hypothèse : aujourd'hui, le « plat prêt » passe aussi par la parole (pas de canal formel) — c'est précisément la source d'erreurs.

## 5. Contraintes et limites

🟦 Hors périmètre V1 : paiement en ligne, stocks, fidélité, multi-restaurant.
🟨 Hypothèse : un seul établissement à Cotonou, une seule caisse.

## 6. Risques

🟩 Risque métier majeur : **résistance au changement** — si l'appli est plus lente que le papier, les serveurs reviendront au papier.
🟩 Risque : la « disponibilité des plats » frôle la gestion des stocks (exclue) — voir contradiction notée par l'Orchestrator.

## 7. Informations manquantes / questions client

1. Combien de tables et de couverts ? Combien de serveurs par service ?
2. Le restaurant dispose-t-il déjà de matériel (tablettes, PC, Wi-Fi, imprimante) ?
3. Quels sont les horaires et pics d'activité (midi, soir) ?
4. Existe-t-il déjà un outil numérique, même partiel (tableur pour la caisse) ?
5. Qui est le décideur final et qui valide les livrables ?
