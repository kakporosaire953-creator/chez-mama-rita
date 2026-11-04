# 09 — Recommandations « contexte béninois » pour les questions Q1–Q14

**Projet :** Chez Mama Rita
**Date :** 2026-11-04
**Source :** recherche documentaire du chef de projet (environnement économique béninois, PME,
secteur restauration, usages numériques, fiscalité) — transmise à l'Orchestrator.
**Statut :** 🟩 **RECOMMANDATIONS FONDÉES SUR LE CONTEXTE LOCAL — NON CONFIRMÉES PAR LE CLIENT.**
Toutes les questions Q1–Q14 restent 🔴 **ouvertes** dans `docs/02-requirements.md` (les réponses
client y sont enregistrées séparément, avec date, par le Business Analyst — R3).

---

## 1. Vérification externe rapide (2026-11-04)

| Affirmation reçue | Vérification | Statut |
|-------------------|--------------|--------|
| Facturation normalisée MECeF / e-MECeF obligatoire au Bénin (DGI, art. 162 bis et 1084-40 du CGI) depuis le 01/07/2021 ; QR code + signature fiscale ; avoir fiscal en cas d'annulation | Confirmée par sources publiques (DGI, presse béninoise, guides 2026) | 🟦 Fait vérifiable — **mais le régime exact de Chez Mama Rita reste à confirmer** (Q3/Q8) |
| Conservation 10 ans des documents comptables (art. 480 CGI Bénin) | Non confirmé spécifiquement pour le Bénin dans nos sources (résultats trouvés : autres pays) | 🟨 Hypothèse — **à confirmer avec le comptable du restaurant** (Q5) |
| ~11,6 M de comptes de services financiers mobiles actifs fin 2025 (ARCEP) | Cohérent avec la généralisation du mobile money au Bénin | 🟨 À sourcer précisément si citée au client |
| Politique nationale PME 2025-2034 / baromètre CCI Bénin 2024 (coûts infrastructures élevés) | Cohérent — justifie de limiter les dépenses matérielles imposées | 🟩 Contexte utile |

## 2. Comparaison avec les exigences existantes et le périmètre V1

### 2.1 Tensions / contradictions potentielles avec le périmètre actuel

| # | Proposition | Tension avec le brief | Analyse |
|---|-------------|----------------------|---------|
| T1 | Q7 : enregistrer les paiements Mobile Money (MTN, Moov, Celtiis…) | Le brief exclut le « paiement mobile **en ligne** » | ✅ **Compatible** si c'est un *enregistrement manuel* par le caissier (pas d'intégration API/online) — à écrire explicitement dans les exigences pour lever l'ambiguïté |
| T2 | Q3/Q8 : facture conforme MECeF/e-MECeF (IFU, QR code, signature fiscale, avoir) | Le brief demande des « factures **simples** » | ⚠️ Tension réelle : une facture normalisée DGI est plus qu'un simple ticket. Si le restaurant est assujetti, c'est une **contrainte légale** qui s'impose ; le régime fiscal de Chez Mama Rita doit être confirmé (nouvelle sous-question pour le client) |
| T3 | Q8 : split bill (par plat / personne / paiement partiel) | Hors des 6 fonctionnalités du brief | ⚠️ Ajout de périmètre potentiel — à valider par le client comme exigence V1 ou V2 |
| T4 | Q9 : menus du jour, demies, suppléments tarifés, options | Enrichit « gestion des plats » | ✅ Dans le périmètre, mais ajoute des exigences (variantes de plats, suppléments) |
| T5 | Q14 : objectif ≤ 5 min de reprise / procédure papier dégradée | Nouvelle exigence non fonctionnelle | ✅ Exigence mesurable, à valider par le client puis testée par le QA |
| T6 | Q5 : conservation 10 ans des documents comptables | Non prévu dans le brief | ⚠️ Nouvelle contrainte légale à confirmer ; ne pas confondre avec la rétention des données personnelles |
| T7 | Q1 : réutiliser le matériel existant, pas de serveur physique imposé | Impacte l'architecture (local vs cloud) | 🟩 Recommandation sage (coûts) — l'Architecte comparera les options en ADR, aucune décision maintenant |

### 2.2 Distinction décisions métier / recommandations techniques

- 🟦 **Décisions métier → validation client requise :** Q2 (moment d'encaissement), Q3/Q8 (facturation
  fiscale, split bill), Q5 (durée de conservation, avec le comptable), Q7 (moyens de paiement acceptés),
  Q9 (variantes de menu), Q10 (politique d'annulation), Q11 (administration des comptes),
  Q13 (recette et mode formation), Q14 (objectif d'indisponibilité accepté).
- 🟩 **Recommandations techniques → décision équipe, argumentée :** Q1 (inventaire matériel, secours
  électrique), Q4 (workflow de disponibilité gérant/cuisine), Q6 (relevé sur place puis dimensionnement),
  Q12 (stratégie de sauvegarde multi-niveaux).

## 3. Avis des agents sollicités

### 3.1 Business Analyst
Les propositions Q2, Q7, Q8 (split bill), Q9, Q10, Q11, Q13 sont des **choix métier du client** :
ils ajoutent ou précisent des exigences (paiement anticipé, moyens de paiement, variantes de plats,
suppléments, politique d'annulation, administrateur) — ils seront formalisés en EF dès confirmation.
Q4 confirme la frontière « disponibilité manuelle ≠ gestion des stocks » (contradiction C1 de la
synthèse 07 résolue dans ce sens, en attente client). Q2 répond à la décision en attente D-01.
**Aucune question n'est clôturée par ces propositions.**

### 3.2 Software Architect
Q1 (réutiliser le matériel, Wi-Fi interne, secours électrique, pas de serveur imposé) et Q14
(fonctionnement hors Internet, reprise ≤ 5 min) orientent vers une architecture **résiliente,
peu coûteuse, autonome localement** — options à comparer en ADR le moment venu (local sur PC
existant, mini-PC, ou cloud hybride), aucune décision prise maintenant. Q12 (sauvegardes
multi-niveaux) et Q5 (rétention 10 ans) deviennent des exigences d'architecture (stockage,
archivage). Q3 (MECeF) implique une **contrainte d'interface fiscale** (génération de facture
normalisée ou connexion SFE approuvée DGI) à étudier si le régime du restaurant l'exige.

### 3.3 QA & Testing
Q14 fournit un critère mesurable (aucune perte de commande ; reprise ≤ 5 min ; bascule papier
numéroté + rapprochement) → cas de test de robustesse. Q3/Q8 → tests de conformité fiscale des
factures (si applicable). Q13 → environnement de formation avec données fictives + recette signée
par 5 profils. Q5 → tests d'archivage/rétention. Q12 → test de restauration obligatoire.
Tous ces critères restent **brouillons** tant que le client n'a pas confirmé.

### 3.4 Security Auditor
Q11 confirme le modèle : comptes individuels, rôles stricts, **désactivation immédiate au départ
avec conservation de l'historique** (audit) — conforme aux règles AGENTS.md. Q12 : les copies de
sauvegarde doivent être protégées (disque externe sécurisé, chiffrement si possible). Q5 :
ne pas confondre rétention légale des pièces comptables (10 ans) et données personnelles —
minimisation pour ces dernières. Q3 : la connexion à un SFE/e-MECeF (si applicable) introduit des
credentials à protéger (jetons API DGI).

## 4. Ce qui nécessite une validation client (prochaine réunion)

1. Régime fiscal du restaurant et applicabilité du MECeF/e-MECeF → format de facture requis (Q3/Q8).
2. Moment d'encaissement + paiement anticipé à emporter (Q2).
3. Moyens de paiement réellement acceptés aujourd'hui (Q7) — espèces + lesquels en mobile money.
4. Split bill souhaité ou non (Q8) ; suppléments/menus du jour/demies (Q9).
5. Politique d'annulation et habilitations (Q10) ; administrateur des comptes (Q11).
6. Durée de conservation validée avec le comptable (Q5).
7. Inventaire matériel + relevé sur place (Q1/Q6) ; objectif d'indisponibilité acceptable (Q14).
8. Recette : signataires et mode formation (Q13) ; support de sauvegarde disponible (Q12).

## 5. Alignement avec l'objectif produit (avis du chef de projet)

🟩 Objectif retenu : ne pas reproduire un logiciel de caisse générique, mais résoudre les **vrais
problèmes** du restaurant — commandes perdues/mal transmises, coordination salle↔cuisine, erreurs
d'encaissement, manque de visibilité du gérant — ce qui est exactement le cœur du brief initial. ✅

---

**Conclusion de l'Orchestrator :** propositions intégrées comme 🟩 recommandations dans
`docs/02-requirements.md` §4.1 ; **les 14 questions restent ouvertes** ; rapport prêt à servir de
support à la prochaine rencontre avec le responsable de Chez Mama Rita. Aucun développement,
aucune décision définitive, phase d'analyse toujours ouverte.
