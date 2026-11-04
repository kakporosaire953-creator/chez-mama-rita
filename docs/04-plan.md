# 04 — Planification du projet

**Projet :** Chez Mama Rita
**Statut :** 🟡 Plan proposé (tâches, dépendances, critères) — **à valider par le chef de projet**
**Mise à jour :** 2026-11-04 (MISSION 06 — conformité énoncé).

> ⚠️ Aucun développement ne démarre avant validation des phases d'analyse (✅ validée),
> d'architecture, de planification et de tests par le chef de projet humain.

## 1. Grandes phases

| Phase | Contenu | Statut |
|-------|---------|--------|
| 0 — Analyse du besoin | Contexte, exigences, workflow | 🟢 Validée (J-007, 2026-11-04) |
| 1 — Réunion client | Réponses Q1–Q14 + SQ-A…SQ-E | 🔴 À faire (SQ-A prioritaire) |
| 2 — Architecture | ADR + décision techno justifiée | 🔴 Après phase 1 |
| 3 — Planification détaillée | Ce document finalisé | 🟡 Proposé |
| 4 — Développement | Application | ⛔ Interdit avant validations |
| 5 — Tests & recette | Exécution des tests préparés + recette client | 🔴 |
| 6 — Déploiement & formation | Mise en service + mode formation | 🔴 |

## 2. Tâches courtes, dépendances, critères d'acceptation (proposition)

| # | Tâche | Agent responsable | Dépend de | Critère d'acceptation |
|---|-------|-------------------|-----------|------------------------|
| T1 | Réunion client + enregistrement réponses Q1–Q14/SQ-A–E | Business Analyst (liaison client) | — | Chaque réponse écrite + datée dans `docs/02-requirements.md` |
| T2 | Figer le catalogue d'exigences (EF/ENF validés) | Business Analyst | T1 | 0 question ouverte impactant le périmètre ; 🟦/🟩 à jour |
| T3 | Revue d'architecture + ADR (choix techno justifié) | Software Architect | T1, T2 | 1 ADR validée dans `docs/07-decisions.md` |
| T4 | Modèle de données final + schéma DB | Software Architect | T3 | Schéma revu par QA + Security |
| T5 | Maquettes/écrans (serveur, cuisine, caisse, dashboard) | BA + Architecte | T2 | 4 écrans validés par le chef de projet |
| T6 | Socle : auth + rôles + comptes | Dev (futur) | T3, T4 | Connexion par rôle testée (TC dans `tests/cases/`) |
| T7 | Menu : plats, prix, disponibilités | Dev | T6 | TC-MENU exécuté ✅ |
| T8 | Commande par table | Dev | T6, T7 | TC-COMMANDE exécuté ✅ |
| T9 | Transmission cuisine temps réel | Dev | T8 | TC-CUISINE exécuté ✅ (délai < cible Q14) |
| T10 | Statuts de commande | Dev | T9 | TC-STATUTS exécuté ✅ |
| T11 | Encaissement + facture | Dev | T10 | TC-ENCAISSEMENT exécuté ✅ (zéro erreur de calcul) |
| T12 | Tableau de bord | Dev | T11 | TC-DASHBOARD exécuté ✅ (totaux = somme des factures) |
| T13 | Exécution des 6 cas de test + rapport | QA & Testing | T7–T12 | 6/6 tests passés, rapport signé |
| T14 | Recette client (5 profils, mode formation) | PO + QA | T13 | Procès-verbal signé (Q13) |
| T15 | Déploiement local + sauvegardes + formation | DevOps/Architecte | T14 | Appli en service, sauvegarde/restauration démontrée |

## 3. Ordre logique

T1 → T2 → T3 → T4 → T5 → T6 → T7 → T8 → T9 → T10 → T11 → T12 → T13 → T14 → T15
(chaîne de dépendances linéaire ; T5 peut être menée en parallèle de T3/T4 après T2).

## 4. Calendrier indicatif

🟨 Brouillon : ~3 mois après validation (6 sprints de 2 semaines) — `docs/brouillons/04-plan-de-travail.md`.

## 5. Références

- `docs/brouillons/04-plan-de-travail.md` (phases, risques) · `docs/06-testing-strategy.md` · `tests/cases/`
