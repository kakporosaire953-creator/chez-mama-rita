# Analyse indépendante — Agent 4 : Expert du domaine restauration (Cotonou, Bénin)

**Projet :** Chez Mama Rita — analyse du besoin
**Date :** 2026-11-04
**Légende :** 🟦 Fait · 🟨 Hypothèse · 🟩 Recommandation

## 1. Problème métier

🟦 Dans la restauration, la valeur se joue sur la **vitesse et l'exactitude du flux de service**. Un plat oublié ou une erreur d'addition coûte directement en temps et en image. Le papier + oral est le maillon faible classique.

## 2. Acteurs (connaissance métier)

🟦 Rôles standards d'un restaurant béninois de quartier/ville, cohérents avec le brief.
🟩 Le **Gérant** est à la fois exploitant et gestionnaire du menu — il doit pouvoir changer un prix ou déclarer une rupture **en cours de service**, sans bloquer la caisse.

## 3. Fonctionnalités (précisions métier)

- 🟩 « Disponibilités » = gestion manuelle des ruptures (ex : « plus de poisson braisé aujourd'hui »), distincte de la gestion de stocks (exclue). La frontière est nette mais doit être communiquée aux utilisateurs.
- 🟩 Statuts de commande : la norme du métier est *reçue → en préparation → prête → servie → payée*.
- 🟩 Facture « simple » = addition de table, en **FCFA (XOF)**, montants entiers — cohérent avec le brief.
- 🟨 Hypothèse : au Bénin, les coupures de courant sont fréquentes → l'outil doit reprendre proprement après une coupure (reprendre la commande là où elle en était).

## 4. Interactions

🟦 Le trio Serveur–Cuisine–Caisse doit être synchronisé : une commande « prête » non signalée bloque le serveur ; une addition éditée après paiement crée des litiges.

## 5. Contraintes

🟦 Pas de paiement mobile en V1 → espèces (et éventuellement chèque/carte manuelle hors appli, à clarifier).
🟨 Hypothèse : TVA et mentions légales sur les tickets — exigences fiscales béninoises à confirmer.

## 6. Risques

🟩 Pics de midi : 10–20 commandes simultanées → l'écran cuisine doit rester lisible.
🟩 Annulation de commande en cours de préparation : source de pertes et de conflits → motif obligatoire + validation gérant (recommandation).
🟩 Changement de prix en cours de journée : doit s'appliquer aux **nouvelles** commandes uniquement.

## 7. Questions client

1. Encaissez-vous uniquement en espèces, ou aussi par carte/virement manuel aujourd'hui ?
2. Proposez-vous des « demies », menus du jour, ou suppléments (ex : sauce en plus) facturés à part ?
3. Faut-il pouvoir découper une addition par personne (split bill) ?
4. Quelles mentions doivent figurer sur le ticket (TVA, nom commercial, adresse) ?
5. Qui a le droit d'annuler une commande ou d'offrir un plat ?
6. Y a-t-il des pourboires gérés par le restaurant ?
