# CHANGELOG.md — Suivi des évolutions de la documentation

**Projet :** Chez Mama Rita
Format : `Version — date — description — auteur — statut de validation`

---

## v0.1.0 — 2026-11-04 — Initialisation du dépôt
- README minimal. — Équipe projet — Validé (commit initial)

## v0.2.0 — 2026-11-04 — Phase 0 : documents de cadrage
- Ajout de `docs/01-vision-et-besoins.md` … `docs/05-plan-de-tests.md`.
- Statut : **brouillons, en attente de validation client**.

## v0.3.0 — 2026-11-04 — Analyse multi-agents du besoin
- Ajout de `docs/analyse/01` à `06` (rapports indépendants) et `07-orchestrateur-synthese.md`.
- 14 questions ouvertes (Q1–Q14) consignées, **aucune résolue**.
- Statut : en attente de validation humaine.

## v0.4.0 — 2026-11-04 — Mise en place de l'équipe d'agents IA
- Ajout de `AGENTS.md`, `agents/` (7 profils), `docs/01-project-context.md` … `docs/07-decisions.md`,
  `templates/` (4 modèles), `tests/README.md`, `journal.md`, `CHANGELOG.md`.
- README réorganisé. Phase d'analyse **toujours ouverte**. Aucun code applicatif.
- Statut : structure validée par le chef de projet (mission d'initialisation).

## v0.5.0 — 2026-11-04 — MISSION 01 : test de l'équipe + application de R1–R5 (validé par le chef de projet)
- Rapport de test : `docs/analyse/08-mission-01-test-fonctionnement-equipe.md` (7/7 agents opérationnels).
- R1 : division des rôles clarifiée (`AGENTS.md` §8 + profils Orchestrator, Critical Reviewer,
  Software Architect, Security Auditor).
- R2 : brouillons de cadrage déplacés vers `docs/brouillons/` (contenus préservés, rien supprimé) ;
  références mises à jour.
- R3 : liaison client confiée au Business Analyst, sous supervision de l'Orchestrator (`AGENTS.md` §9).
- R4 : Definition of Done par livrable (`AGENTS.md` §10).
- R5 : journalisation (J-005, J-006).
- **R6 reporté par décision du chef de projet** : aucun nouvel agent UX/DevOps pour le moment.
- Phase d'analyse toujours ouverte. Aucun code applicatif.

## v0.6.0 — 2026-11-04 — Propositions « contexte béninois » pour Q1–Q14 (recommandations, non confirmées)
- `docs/02-requirements.md` §4.1 : propositions du chef de projet ajoutées à côté des questions
  ouvertes — **les 14 questions restent 🔴 ouvertes**, aucune réponse client enregistrée.
- Rapport d'analyse : `docs/analyse/09-recommandations-contexte-beninois.md` (avis BA, Architecte, QA,
  Sécurité ; tensions avec le périmètre ; support pour la prochaine réunion client).
- Aucun développement. Phase d'analyse ouverte.

## v0.7.0 — 2026-11-04 — Validation humaine de la phase d'analyse métier
- Le chef de projet valide l'analyse métier (rapports `docs/analyse/10` à `13`, verdict MISSION 05 : **VALIDÉ**).
- Enregistré dans `journal.md` (J-007) et `docs/07-decisions.md` (D-VAL-01).
- Q1–Q14 et SQ-A…SQ-E restent ouvertes ; aucune architecture définitive ; aucun développement.

## v0.8.0 — 2026-11-04 — MISSION 06 : conformité à l'énoncé (corrections autorisées)
- Livrables renommés : `docs/01-comprehension.md`, `02-acteurs-et-interactions.md`, `03-architecture.md`,
  `04-plan.md` + nouveau `docs/05-workflow.md` ; références mises à jour dans tout le dépôt.
- Ajouts : diagramme Mermaid (acteurs/interactions), README « lancer le workflow », AGENTS.md §11–12
  (actions autorisées sans validation, méthodes de test), architecture à options justifiées 🟩,
  plan de 15 tâches avec dépendances/critères, 6 cas de test préparés dans `tests/cases/` (non exécutés),
  `LINKEDIN.md` (brouillon).
- Audit : `docs/analyse/15-audit-conformite-enonce.md` (verdict : CONFORME SOUS RÉSERVES).
- Dépôt GitHub public vérifié (API) ; branche pushée. Q1–Q14/SQ-A–E ouvertes. Aucun développement.

---

<!-- Ajouter une entrée par modification importante validée, ex. :
## vX.Y.Z — AAAA-MM-JJ — Titre
- Description. — Auteur — Validé le … par …
-->
