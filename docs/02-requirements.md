# 02 — Exigences (fonctionnelles et non fonctionnelles)

**Projet :** Chez Mama Rita
**Statut :** 🟡 En cours d'analyse — **À valider**
**Dernière mise à jour :** 2026-11-04

> Règle : aucune exigence n'est inventée. Toute ambiguïté devient une question ouverte (section 4).
> Ne pas considérer les questions comme résolues sans réponse écrite du client.

## 1. Exigences fonctionnelles — 🟡 À analyser / À valider

| ID | Exigence (brouillon issu du brief) | Priorité | Statut |
|----|-----------------------------------|----------|--------|
| EF-01… | Gestion des plats, prix, disponibilités | À définir | 🟡 À valider |
| EF-… | Prise de commandes par table | À définir | 🟡 À valider |
| EF-… | Transmission automatique à la cuisine | À définir | 🟡 À valider |
| EF-… | Suivi des statuts des commandes | À définir | 🟡 À valider |
| EF-… | Paiements et factures simples | À définir | 🟡 À valider |
| EF-… | Tableau de bord ventes / plats populaires | À définir | 🟡 À valider |

🟨 Un premier découpage détaillé (EF-01 à EF-29, priorités MoSCoW) existe à l'état de **brouillon**
dans `docs/brouillons/02-exigences.md` — il est **à valider** et peut évoluer avec les réponses du client.

## 2. Exigences non fonctionnelles — 🟡 À analyser

- Non défini de manière validée. Brouillon disponible dans `docs/brouillons/02-exigences.md` (ENF-01 à ENF-10).

## 3. Matrice acteurs × fonctionnalités — 🟡 À analyser

- Voir brouillon dans `docs/brouillons/02-exigences.md` §3.

## 4. Questions ouvertes en attente du client (Q1–Q14)

> **Aucune de ces questions n'est résolue.** La colonne « Réponse du client » est volontairement
> vide : elle est destinée à enregistrer les réponses futures du client, avec leur date.

| # | Question | Statut | Réponse du client | Date de réponse |
|---|----------|--------|-------------------|-----------------|
| Q1 | Quels appareils existent déjà (tablettes, PC, écran cuisine, imprimante) et quelles tailles ? Wi-Fi fiable ? Local verrouillable pour le serveur ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q2 | Encaissement autorisé dès « prête » ou seulement après « servie » ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q3 | Impression des tickets (imprimante disponible ?) ou génération PDF ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q4 | La « disponibilité » se limite-t-elle à une rupture déclarée manuellement par le gérant (pas de stock décrémenté automatiquement) ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q5 | Durée de conservation des commandes et factures (obligation légale béninoise) ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q6 | Nombre de tables, couverts, serveurs par service, volume de commandes en pic de midi ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q7 | Encaissement : espèces uniquement, ou aussi carte/virement manuel traité hors appli ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q8 | Mentions obligatoires sur la facture (TVA, adresse, n° fiscal) ? Split bill (addition par personne) ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q9 | Menus du jour, « demies », suppléments facturés à part ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q10 | Qui peut annuler une commande, à quel stade, motif obligatoire ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q11 | Qui administre les comptes utilisateurs ? Procédure en cas de départ d'un employé ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q12 | Quel support de sauvegarde disponible sur place (clé USB, disque externe, NAS) ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q13 | Qui exécute et signe la recette côté client ? Mode « formation » avec données fictives ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |
| Q14 | Temps d'indisponibilité maximum acceptable en plein service ? | 🔴 Ouverte | *(à remplir)* | *(à remplir)* |

### 4.1 Propositions fondées sur le contexte local béninois (2026-11-04) — 🟩 RECOMMANDATIONS, NON confirmées par le client

> Source : recherche documentaire du chef de projet (contexte économique béninois, PME, restauration,
> fiscalité). Ces propositions sont enregistrées ici **sans clôturer les questions** : le statut de
> chaque question reste 🔴 **Ouverte** et la colonne « Réponse du client » reste vide tant que le
> responsable de Chez Mama Rita n'a pas confirmé par écrit. Analyse détaillée :
> `docs/analyse/09-recommandations-contexte-beninois.md`.

| # | Proposition (résumé) | Type | Validation requise |
|---|----------------------|------|--------------------|
| Q1 | Inventaire du matériel existant ; smartphones/tablettes serveurs, écran cuisine, poste caisse ; Wi-Fi interne couvrant salles/cuisine/caisse ; secours électrique ; pas de serveur physique imposé | 🟩 Recommandation technique | Client (inventaire réel) + architecte |
| Q2 | Encaissement définitif après « servie » ; statuts Reçue → En préparation → Prête → Servie → Payée ; paiement anticipé possible (à emporter) | 🟦 Décision métier | **Client** |
| Q3 | Impression ticket de préparation si imprimante + facture conforme + copie numérique ; tenir compte du MECeF/e-MECeF (DGI) | 🟦 Décision métier + contrainte fiscale | **Client + comptable** (régime fiscal) |
| Q4 | Disponibilité gérée manuellement par le gérant ; le responsable cuisine peut signaler une rupture ; pas de stock automatique | 🟩 Recommandation (dans le périmètre) | **Client** (confirmer le workflow) |
| Q5 | Conservation 10 ans des documents comptables (factures, pièces justificatives) — à confirmer auprès du comptable du restaurant | 🟦 Contrainte légale | **Client + comptable** |
| Q6 | Ne pas inventer de chiffres : relevé sur place (tables, places, serveurs, volume pic, plats/commande, temps prise→service) | 🟩 Méthode | **Client** (relevé sur place) |
| Q7 | Enregistrer espèces + MTN MoMo + Moov + Celtiis + virement + carte (si terminal) — **enregistrement manuel**, l'intégration en ligne reste hors périmètre | 🟦 Décision métier | **Client** (moyens réellement acceptés) |
| Q8 | Facture avec identification restaurant + IFU, n°, date, plats, quantités, prix, taxes, total ; TVA selon régime réel ; split bill (par plat/personne/paiement partiel) prévu | 🟦 Décision métier | **Client + comptable** |
| Q9 | Prévoir menu du jour, demi-portion/portion, suppléments tarifés, options (« sans piment ») | 🟦 Décision métier (nouvelles exigences) | **Client** |
| Q10 | Annulation : serveur avant envoi cuisine ; après envoi = autorisation gérant ; motif obligatoire si préparation commencée ; historique obligatoire ; facture émise = avoir fiscal, pas de suppression | 🟦 Décision métier | **Client** |
| Q11 | Gérant = administrateur principal ; compte individuel par employé ; désactivation immédiate au départ, historique conservé ; rôles par fonction | 🟦 Décision métier + sécurité | **Client** |
| Q12 | Sauvegardes automatiques multi-niveaux : quotidienne + copie locale disque externe + copie distante si Internet + tests de restauration périodiques (pas une simple clé USB seule) | 🟩 Recommandation technique | Équipe (avec support client Q12) |
| Q13 | Recette signée par propriétaire/gérant + représentants serveurs/cuisine/caissier + chef de projet technique ; mode formation avec données fictives | 🟦 Décision métier | **Client** |
| Q14 | Objectif : aucune perte de commande enregistrée ; fonctionnement hors Internet ; reprise/procédure papier en ≤ 5 min max (tickets papier numérotés, rapprochement ultérieur) | 🟩 Recommandation technique (objectif à faire accepter) | **Client** (accepter l'objectif) + QA (tests) |

## 5. Références

- Synthèse Orchestrator : `docs/analyse/07-orchestrateur-synthese.md` §5
- Propositions « contexte béninois » : `docs/analyse/09-recommandations-contexte-beninois.md`
- Brouillon détaillé : `docs/brouillons/02-exigences.md`
