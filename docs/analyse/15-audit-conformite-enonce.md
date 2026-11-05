# 15 — MISSION 06 : Audit global de conformité à l'énoncé

**Date :** 2026-11-04 · **Date limite exercice :** vendredi 2026-11-06 à 18 h
**Référentiel :** exigences de l'énoncé « enonce-exercice-workflow-agents-ia.pdf » (PDF non présent
au dépôt ; référentiel utilisé = liste A–J de la mission). Vérifications faites **directement dans
le dépôt** + API GitHub pour la publication.
**Règles respectées :** aucun fichier modifié/supprimé/renommé ; un seul fichier créé (celui-ci) ;
aucun développement ; aucun test déclaré exécuté ; aucune décision métier rouverte.

---

## 1. Résumé exécutif

Le dépôt contient une **analyse métier validée et traçée** (rapports 10–13, verdict VALIDÉ), un
**workflow d'agents documenté** (AGENTS.md + 7 profils), un **journal complet** (J-001…J-007 avec
validations humaines) et un **dépôt GitHub public vérifié**. Les écarts à l'énoncé portent surtout
sur : les **noms de fichiers attendus** (01-comprehension.md, 02-acteurs-et-interactions.md,
03-architecture.md, 04-plan.md, 05-workflow.md), l'**absence de diagramme Mermaid**, l'**absence
de tests préparés** dans `tests/`, des **précisions manquantes** dans README/AGENTS.md (lancement du
workflow, actions autorisées sans validation, méthodes de test), et les **éléments LinkedIn**.

> **Verdict : 🟡 CONFORME SOUS RÉSERVES** — le fond est conforme ; des compléments ciblés sont
> nécessaires avant le 2026-11-06 18 h (voir §9 et §10).

## 2. Tableau de conformité par livrable de l'énoncé

| Élément de l'énoncé | Statut | Justification |
|---------------------|--------|---------------|
| A. README.md (présentation, structure, lancement du workflow) | 🟡 Partiellement conforme | Présentation ✅, structure ✅, méthode ✅ ; mais pas d'instructions étape par étape pour « lancer le workflow » |
| B. AGENTS.md (rôles, conventions, actions autorisées sans validation, actions avec validation, méthodes de test) | 🟡 Partiellement conforme | Conventions ✅, validations humaines ✅, rôles ✅ (via `agents/`) ; **liste explicite des actions autorisées sans validation** ❌ ; méthodes de test/vérification 🟡 (DoD présent, stratégie dans `docs/06`) |
| C. Compréhension du besoin (reformulation, questions ouvertes, hypothèses) | 🟡 Partiellement conforme | Contenu ✅ (docs/01, docs/02 §4, analyse/10) mais fichier attendu `docs/01-comprehension.md` — nom différent |
| D. Acteurs et interactions (4 acteurs, responsabilités, interactions, **diagramme Mermaid**) | 🟡 Partiellement conforme | 4 acteurs + responsabilités + interactions ✅ (analyse/10 §1, docs/03) ; **diagramme Mermaid 🔴 absent** (0 occurrence de « mermaid » dans le dépôt) |
| E. Architecture (choix justifiés, modèle de données, arborescence cible, raisons) | 🟡 Partiellement conforme | Propositions justifiées + modèle de données dans `docs/brouillons/03` (non validées, par règle du projet) ; `docs/03-architecture.md` est volontairement « Non défini » ; **arborescence cible absente** ; nom attendu `03-architecture.md` différent |
| F. Planification (tâches courtes, critères d'acceptation, dépendances, ordre) | 🟡 Partiellement conforme | Phases/sprints dans `docs/brouillons/04` ; `docs/04-plan.md` en attente (tâches détaillées, dépendances et critères par tâche non rédigés) ; nom attendu `04-plan.md` différent |
| G. Workflow des agents (étapes, responsabilités, délégation, contrôles humains, erreurs/désaccords) | 🟡 Partiellement conforme | Contenu ✅ réparti dans `AGENTS.md` + `agents/*.md` (délégation, escalade, gestion des désaccords) ; mais pas de fichier unique `docs/05-workflow.md` |
| H. tests/ (≥ 1 test par fonctionnalité principale : menu, commande, transmission cuisine, statuts, encaissement/facturation, tableau de bord) | 🔴 Absent | `tests/` contient uniquement `README.md` ; **aucun test préparé** (autorisé avant le code, mais rien n'existe) |
| I. journal.md (échanges, missions, décisions, validations humaines) | ✅ Conforme | J-001…J-007 : missions, rapports, corrections, décisions, validations (J-007) |
| J. Publication (dépôt public GitHub/GitLab vérifié + préparation LinkedIn) | 🟡 Partiellement conforme | ✅ Dépôt **public vérifié via API GitHub** : `visibility: public`, https://github.com/kakporosaire953-creator/chez-mama-rita — ⚠️ mais le contenu des missions est **non pushé** (branche locale) ; 🔴 éléments LinkedIn (démarche, apprentissages, difficultés, résultats, lien) **non préparés** |

## 3. Correspondance fichiers existants ↔ fichiers attendus par l'énoncé

| Fichier attendu (énoncé) | Fichier(s) existant(s) équivalent(s) | Note |
|--------------------------|--------------------------------------|------|
| README.md | `README.md` | ✅ même nom |
| AGENTS.md | `AGENTS.md` | ✅ même nom |
| docs/01-comprehension.md | `docs/01-comprehension.md` + `docs/02-requirements.md` + `docs/analyse/10-…` | contenu présent, nom différent |
| docs/02-acteurs-et-interactions.md | `docs/02-acteurs-et-interactions.md` + `docs/analyse/10` §1 | contenu présent ; Mermaid manquant |
| docs/03-architecture.md | `docs/03-architecture.md` (vide, volontaire) + `docs/brouillons/03-architecture-et-donnees.md` | propositions non validées par règle projet |
| docs/04-plan.md | `docs/04-plan.md` + `docs/brouillons/04-plan-de-travail.md` | détaillé à produire |
| docs/05-workflow.md | `AGENTS.md` + `agents/*.md` | contenu réparti |
| tests/ | `tests/README.md` seul | tests à préparer |
| journal.md | `journal.md` | ✅ |

## 4. Éléments conformes ✅

- Journal complet et traçable (missions, décisions, validations humaines J-007).
- Analyse métier validée (verdict MISSION 05 : VALIDÉ) avec séparation faits/hypothèses/propositions.
- Workflow multi-agents documenté et testé (MISSION 01 : 7/7 agents opérationnels).
- Gouvernance : validation humaine obligatoire, questions ouvertes conservées (Q1–Q14, SQ-A…E).
- Dépôt GitHub public vérifié par API (pas de prétention non vérifiée).

## 5. Éléments partiellement conformes 🟡

- README (instructions de lancement du workflow), AGENTS.md (actions autorisées sans validation,
  méthodes de test), noms de fichiers docs/01…05, diagramme Mermaid, plan détaillé, arborescence
  cible, push du contenu, LinkedIn.

## 6. Éléments absents 🔴

- **Diagramme Mermaid** (acteurs/interactions).
- **Tests préparés** dans `tests/` (6 fonctionnalités principales sans aucun cas de test).
- **Éléments LinkedIn** (démarche, apprentissages, difficultés, résultats, lien du dépôt).
- Liste explicite dans AGENTS.md des **actions autorisées sans validation humaine**.

## 7. Anomalies et risques

| Risque | Détail |
|--------|--------|
| R-1 | Contenu des missions non pushé → le dépôt public ne montre que le commit initial ; la démo à la date limite dépend d'un push (à autoriser) |
| R-2 | Noms de fichiers docs/01…05 différents de l'énoncé → risque de non-conformité formelle si l'énoncé est strict sur les noms |
| R-3 | `docs/analyse/` (13 rapports) + `docs/brouillons/` (5) : redondance partielle avec `docs/01…07`, mais **non contradictoire** (audit 13) — garder pour la traçabilité, ne pas supprimer |
| R-4 | Architecture volontairement non décidée (règle projet : pas de techno sans validation client) vs énoncé demandant des choix justifiés → à concilier : présenter les **options justifiées** (brouillon 03) comme livrable d'architecture préparatoire, sans décision définitive |
| R-5 | Aucun test déclaré exécuté ✅ (conforme à la règle) — mais il faut les **préparer** |

## 8. Corrections nécessaires (liste, sans exécution — autorisation requise)

1. Préparer dans `tests/` ≥ 1 cas de test par fonctionnalité principale (6) — QA & Testing.
2. Ajouter un **diagramme Mermaid** acteurs/interactions (dans le doc acteurs ou un doc dédié).
3. README : ajouter une section « Comment lancer le workflow » (étapes concrètes).
4. AGENTS.md : ajouter la liste des **actions autorisées sans validation humaine** et les **méthodes de test/vérification**.
5. Aligner les noms des livrables de l'énoncé (01-comprehension.md, 02-acteurs-et-interactions.md,
   03-architecture.md, 04-plan.md, 05-workflow.md) — par renommage ou fichiers de correspondance.
6. Rédiger le plan détaillé (tâches courtes, critères d'acceptation, dépendances, ordre) — Project Planner.
7. Push de la branche sur le dépôt public (avec autorisation).
8. Rédiger le brouillon de post LinkedIn (démarche, apprentissages, difficultés, résultats, lien).

## 9. Priorisation des tâches restantes

- **A. Indispensable avant le 2026-11-06 18 h :** 1 (tests), 2 (Mermaid), 3 (README), 4 (AGENTS.md),
  5 (noms des livrables), 7 (push), 8 (LinkedIn). Le 6 (plan détaillé) est strongly recommandé.
- **B. Améliorations facultatives :** plan détaillé complet (6), arborescence cible (dans 03),
  consolidation des rapports d'analyse, documentation des ADR futurs.
- **C. Hors priorité :** tout développement, tout choix technologique définitif, la clôture des
  questions Q1–Q14/SQ-A…E sans le client, la création de nouveaux agents (R6 reporté).

## 10. Verdict final

> ### 🟡 **CONFORME SOUS RÉSERVES**
>
> Fond conforme (analyse validée, workflow, journal, dépôt public vérifié). Réserves : tests
> préparés absents, diagramme Mermaid absent, noms de livrables à aligner, précisions
> README/AGENTS.md, push du contenu et préparation LinkedIn.

⏸️ **Audit terminé — en attente de l'autorisation du chef de projet avant toute correction.**
