# 10 — MISSION 02 : Analyse approfondie du besoin métier (version corrigée MISSION 04)

**Projet :** Chez Mama Rita (Cotonou, Bénin)
**Date :** 2026-11-04 — corrigé le 2026-11-04 selon l'audit `docs/analyse/11-audit-rapport-analyse-metier.md`
(anomalies F-01 à F-11 traitées ; rapport de corrections : `docs/analyse/12-rapport-corrections-mission-04.md`)
**Responsable principal :** Business Analyst · **Contributeurs :** QA & Testing, Security Auditor,
Critical Reviewer · **Consolidation :** Orchestrator
**Statut :** 🟡 Rapport proposé — **en attente d'approbation du chef de projet**

**Légende :**
- 🟦 **Fait** — énoncé par le brief/client
- 🟨 **Hypothèse / impliqué** — non dit explicitement, mais nécessaire au fonctionnement des 6 familles du brief ; à vérifier
- 🟩 **Proposition** — déduction, ajout ou recommandation de l'équipe ; **jamais présentée comme confirmée par le client**

**Origine des exigences (MISSION 04) :** 🟦 Direct = découle explicitement d'une des 6 familles du brief ·
🟨 Impliqué = nécessaire au fonctionnement d'une famille du brief · 🟩 Proposé = ajout/déduction au-delà du brief (à valider).

---

## 0. Sources utilisées

- Brief initial du client (contexte, 4 acteurs, 6 familles fonctionnelles, 4 exclusions)
- `docs/01-comprehension.md`, `docs/02-requirements.md` (+ §4.1 propositions, questions ouvertes Q1–Q14)
- `docs/analyse/01` à `09` et `11` (rapports, synthèse, recommandations « contexte béninois », audit MISSION 03)
- `docs/brouillons/02-exigences.md` (EF-01…29, ENF-01…10 — brouillon de travail, non validé)

---

## 1. Cartographie des acteurs

| Acteur | Rôle métier | Responsabilités | Difficultés actuelles 🟦 |
|--------|-------------|-----------------|--------------------------|
| **Serveur** | Prend les commandes des tables, sert, suit l'avancement | Saisie, transmission, service | Papier + transmission orale → commandes perdues/mal transmises ; pas de visibilité sur les plats prêts |
| **Cuisinier** | Reçoit et prépare les commandes | Préparation | Réception orale uniquement → oublis, aucune trace |
| **Caissier** | Établit et encaisse les factures | Facturation, encaissement | Facturation manuelle → **erreurs constatées par le client** |
| **Gérant** | Supervise, gère le menu, exploite l'activité | Pilotage | Aucune vision consolidée des ventes |

🟨 Hypothèse (proposition Q1, **non confirmée**) : trois salles + cuisine + caisse. À confirmer (Q1/Q6/SQ-B).

## 2. Processus métier

### 2.1 AS-IS (uniquement des faits documentés 🟦)

```
[Client] → [Serveur] note sur PAPIER → transmet ORALEMENT à la [Cuisine]
→ [Cuisinier] prépare → [Serveur] sert → [Caissier] calcule la facture MANUELLEMENT
← erreurs constatées → encaissement → clôture de la table
[Gérant] : aucune vision consolidée
```

🟨 Non documenté (ne pas inventer) : nb de tables, serveurs/service, moyens de paiement, imprimante,
régime fiscal, horaires de pic → questions Q1–Q14 / SQ-A…SQ-E.

### 2.2 TO-BE (🟩 proposition globale, non validée)

Commande par table dans l'appli → transmission automatique temps réel à l'écran cuisine →
statuts suivis (liste des statuts = 🟩 Q2) → facture calculée automatiquement → encaissement →
clôture → tableau de bord pour le gérant.

## 3. Catalogue des exigences fonctionnelles (avec origine — correction F-01)

Les 6 familles du brief 🟦 : (1) plats/prix/disponibilités, (2) commande par table,
(3) transmission auto cuisine, (4) statuts, (5) paiements/factures simples, (6) tableau de bord.

| EF | Exigence (résumé) | Origine | Précision |
|----|-------------------|---------|-----------|
| EF-01 | Créer un plat (nom, prix, etc.) | 🟦 (1) | description/photo/catégorie = 🟩 détail |
| EF-02 | Modifier prix/description | 🟦 (1) | règle « prix figé aux anciennes commandes » = 🟩 |
| EF-03 | Supprimer/**archiver** un plat | 🟩 | ajout au-delà du brief |
| EF-04 | Disponible / indisponible (rupture) | 🟦 (1) | workflow gérant/cuisine = 🟩 Q4 |
| EF-05 | Catégories de plats | 🟩 | organisation ajoutée |
| EF-06 | Gérer les tables (n°, capacité, zone) | 🟨 (2) | les tables sont nécessaires à « par table » ; détails zone/capacité = 🟩 |
| EF-07 | Vue d'ensemble de l'état des tables | 🟨 (2)+(4) | découle de la commande par table + suivi |
| EF-08 | Ouvrir une commande sur une table, rattachée au serveur | 🟦 (2) | |
| EF-09 | Ajouter des plats (quantité, commentaire) | 🟦 (2) | commentaire « sans piment » = 🟩 détail (lié Q9) |
| EF-10 | Modifier/supprimer une ligne avant envoi | 🟨 (2) | cohérence de saisie |
| EF-11 | Envoyer la commande à la cuisine | 🟦 (3) | |
| EF-12 | Commande complémentaire après envoi | 🟩 | proposition |
| EF-13 | Affichage auto écran cuisine | 🟦 (3) | tri par ancienneté = 🟩 détail |
| EF-14 | Statuts de commande | 🟦 (4) | la liste exacte des 5 statuts = 🟩 Q2 |
| EF-15 | Cuisinier marque « en préparation »/« prêt » | 🟦 (4) | |
| EF-16 | Serveur marque « servie » | 🟨 (4) | transition exacte selon Q2 |
| EF-17 | Annuler une commande avec motif | 🟩 | politique d'annulation = 🟩 Q10 |
| EF-18 | Facture automatique (plats, quantités, total) | 🟦 (5) | « zéro erreur d'arrondi » = critère QA |
| EF-19 | Encaisser en espèces, montant reçu, rendu auto | 🟨 (5) | « espèces » = hypothèse de base ; moyens réels = Q7/SQ-D 🟩 |
| EF-20 | Facture avec n°, date, heure (impression/PDF) | 🟨 (5) | format (ticket/PDF) = Q3 ; conformité MECeF = SQ-A 🟩 |
| EF-21 | Réimprimer / consulter les factures passées | 🟩 | ajout (audit F-01) |
| EF-22 | Clôturer la table après paiement | 🟨 (5) | |
| EF-23 | Chiffre d'affaires par période | 🟦 (6) | |
| EF-24 | Nombre de commandes / couverts | 🟨 (6) | |
| EF-25 | Top des plats les plus commandés | 🟦 (6) | |
| EF-26 | Ventes par catégorie et par serveur | 🟩 | ajout (audit F-01) |
| EF-27 | Connexion + rôles (4 acteurs) | 🟨 | les 4 acteurs sont 🟦, le contrôle d'accès formel est 🟨 |
| EF-28 | Gérant crée/désactive les comptes | 🟩 | modalités = Q11 |
| EF-29 | Journal des actions sensibles | 🟩 | exigence de sécurité proposée (audit F-01) |

**Bilan MISSION 04 :** 🟦 direct : EF-01, 02, 04, 08, 09, 11, 13, 14, 15, 18, 23, 25 (12) ·
🟨 impliqué : EF-06, 07, 10, 16, 19, 20, 22, 24, 27 (9) · 🟩 proposé : EF-03, 05, 12, 17, 21, 26, 28, 29 (8).

### ENF (brouillon) — origines

🟨 ENF-01 (hors Internet), ENF-02 (délai < 3 s : valeur 🟨 à confirmer via Q14/Q6, critère à fixer),
ENF-03 (simplicité), ENF-04 (responsive), ENF-08 (multi-utilisateurs), ENF-10 (français/XOF 🟨 à valider) ·
🟩 ENF-05 (détails sécurité), ENF-06 (sauvegarde — lié Q12), ENF-07 (rétention : durée = Q5/SQ-C 🟩),
ENF-09 (impression — Q3).

## 4. Cas d'utilisation (avec origine — correction F-02)

| UC | Cas d'utilisation | Acteur | Origine | Notes |
|----|-------------------|--------|---------|-------|
| UC-01 | Gérer le menu (plats, prix, disponibilité) | Gérant | 🟦 (1) | rupture signalée par la cuisine = 🟩 Q4 |
| UC-02 | Gérer tables/salles | Gérant | 🟨 (2) | nb de salles = 🟨 SQ-B |
| UC-03 | Prendre une commande par table | Serveur | 🟦 (2) | commentaire = 🟩 (Q9) |
| UC-04 | Transmettre la commande à la cuisine | Serveur | 🟦 (3) | délai mesurable : à fixer (Q14) |
| UC-05 | Suivre la préparation, changer les statuts | Cuisinier | 🟦 (4) | statuts exacts = 🟩 Q2 |
| UC-06 | Marquer la commande servie | Serveur | 🟨 (4) | transition selon Q2 |
| UC-07 | Encaisser et clôturer la table | Caissier | 🟦 (5) | **précondition « après servie » = 🟩 Q2, non validée** |
| UC-08 | Consulter le tableau de bord | Gérant | 🟦 (6) | |
| UC-09 | Gérer les comptes utilisateurs | Gérant/Admin | 🟩 | issu du brouillon (EF-27…29) + Q11, **pas du brief** |
| UC-10 | Annuler une commande | Serveur/Gérant | 🟩 | politique = Q10 |
| UC-11 | Mode formation (données fictives) | Tous | 🟩 | Q13 |

✅ **Affirmation corrigée (F-02)** : les 6 familles du brief justifient directement
UC-01, UC-03, UC-04, UC-05, UC-07, UC-08 (🟦) et impliquent UC-02, UC-06 (🟨).
**UC-09, UC-10, UC-11 proviennent de propositions/brouillons (🟩)** et ne sont pas des besoins
confirmés par le client.

## 5. Exceptions et risques opérationnels

| ID | Exception / risque | Règle proposée 🟩 (à valider) |
|----|--------------------|-------------------------------|
| EX-01 | Plat indisponible après commande (lien UC-01) | Ligne conservée ; plat grisé ensuite |
| EX-02 | Annulation après envoi cuisine (lien UC-10) | Autorisation gérant + motif + historique (Q10) |
| EX-03 | Coupure Wi-Fi/élec/panne | Procédure papier numéroté, reprise ≤ 5 min, rapprochement (Q14) |
| EX-04 | Double envoi (double clic) | Déduplication/confirmation (scénario QA) |
| EX-05 | Erreur de saisie avant envoi | Correction de ligne (EF-10) |
| EX-06 | Paiement partiel / addition partagée | Split bill 🟩 Q8 |
| EX-07 | Départ d'un employé | Désactivation immédiate, historique conservé 🟩 Q11 |
| EX-08 | Facture émise à corriger | Avoir fiscal, jamais de suppression 🟩 SQ-A/Q8 |
| R-OP1 | Pic de midi | Performance à tester (Q6/Q14) |
| R-OP2 | Retour au papier (adoption) | Simplicité + formation |
| R-OP3 | Perte de données | Sauvegardes multi-niveaux + restauration testée 🟩 Q12 |

## 6. Éléments examinés en MISSION 04 — classification (correction D, aucun intégré comme exigence)

| Élément | Classification | Détail |
|---------|----------------|--------|
| Clôture journalière de caisse (rapport Z) | 🟩 **Proposition métier pertinente à soumettre au client** (hors brief explicite) | Candidate UC-12, en attente Q13 |
| Impression du ticket cuisine | 🟩 **Proposition** liée à Q3 | À soumettre au client |
| Plusieurs commandes sur une même table | 🟩 **Proposition** (liée à EF-12, commande complémentaire) | À soumettre au client |
| Sauvegarde et restauration | 🟩 **Recommandation technique** (Q12) → à formaliser en ENF, pas en UC métier | |
| Concurrence entre utilisateurs (2 serveurs, même table) | 🟩 **Scénario de test QA** (lié ENF-08), pas une exigence métier | |

Aucun de ces éléments n'est « déjà justifié par le brief » tel quel ; aucun n'est hors périmètre
définitivement — tous restent 🟩 en attente de validation client.

## 7. Questions ouvertes (inchangées — restent ouvertes 🔴)

Q1–Q14 (`docs/02-requirements.md`) + sous-questions SQ-A (régime fiscal/MECeF), SQ-B (salles),
SQ-C (comptable/rétention), SQ-D (moyens de paiement réels), SQ-E (à emporter/paiement anticipé).
**Aucune n'a été résolue artificiellement.**

## 8. Avis des contributeurs (post-correction)

- **QA & Testing** : chaque EF 🟦/🟨 devra recevoir un critère d'acceptation mesurable après
  réponses client (Q2, Q6, Q7, Q8, Q14) ; scénarios prioritaires : UC-03→UC-07 bout en bout,
  EX-03 panne, EX-04 doublon, EX-08 avoir, concurrence (ENF-08), sauvegarde/restauration (Q12).
- **Security Auditor** : matrice rôles × actions = 🟩 **proposée, à valider (Q11)** ; journal d'audit
  (EF-29 🟩) à confirmer ; comptes individuels, désactivation immédiate (EX-07).
- **Software Architect** : contraintes fonctionnelles identifiées sans choix techno : temps réel
  (UC-04), hors-ligne (ENF-01), multi-postes (ENF-04/08), interface fiscale si SQ-A positif,
  rétention (Q5), volumétrie (Q6).
- **Critical Reviewer** : F-01/F-02 corrigés ; UC-09/10/11 bien marqués 🟩 ; plus de
  présentation de propositions comme des faits ; doublon UC-01/EX-01 supprimé (renvoi croisé).

## 9. Recommandations pour la validation métier

1. Réunion client : SQ-A en priorité (fiscalité), puis Q2, Q3, Q7, Q8, Q9, Q10, Q11, Q13, Q14,
   inventaire matériel + relevé sur place (Q1/Q6), confirmation comptable (Q5/SQ-C).
2. Le Business Analyst (liaison client, R3) enregistre chaque réponse avec date dans
   `docs/02-requirements.md` ; seule une réponse écrite clôture une question.
3. Après validation client : figer le catalogue EF/ENF, puis revue d'architecture (ADR).

---

# Synthèse Orchestrator (version corrigée)

Analyse cohérente et traçable : chaque EF et chaque UC a une **origine identifiable** (🟦/🟨/🟩) ;
les contradictions majeures F-01/F-02 sont corrigées ; les 14 questions + SQ-A…SQ-E restent
ouvertes ; aucune proposition présentée comme confirmée ; périmètre respecté.

⏸️ **En attente d'approbation du chef de projet.** Aucun développement, aucune technologie choisie.
