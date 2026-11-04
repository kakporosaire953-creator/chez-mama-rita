# 05 — Workflow des agents IA

**Projet :** Chez Mama Rita · **Mise à jour :** 2026-11-04 (MISSION 06 — conformité énoncé)
Règles détaillées : `AGENTS.md` · Profils : `agents/` (7 agents)

## 1. Les étapes du workflow

```
1. MISSION      Orchestrator rédige la fiche (templates/agent-mission.md) → journal.md
2. RÉALISATION  L'agent responsable produit son rapport (templates/analysis-report.md)
3. REVUE        Critical Reviewer émet un avis critique (ne bloque pas)
4. CONSOLIDATION Orchestrator consolide, détecte les contradictions
5. VALIDATION   Chef de projet humain valide (obligatoire pour toute décision importante)
6. ARCHIVAGE    journal.md + CHANGELOG.md + ADR (docs/07-decisions.md) si décision
```

## 2. Responsabilités des agents

| Agent | Rôle dans le workflow |
|-------|----------------------|
| Orchestrator | Distribue les missions, consolide, escalade — **ne décide pas à la place du chef de projet** |
| Business Analyst | Analyse le besoin, exigences, liaison client (réponses Q1–Q14) |
| Software Architect | Étudie les options, ADR — aucune décision techno sans validation |
| Project Planner | Phases, tâches, dépendances, calendrier |
| QA & Testing | Stratégie de test, cas préparés (`tests/cases/`), recette |
| Security Auditor | Permissions, risques, traçabilité, sauvegardes |
| Critical Reviewer | Revue indépendante, détecte incohérences et oublis |

## 3. Mécanismes de délégation

- L'Orchestrator délègue via une **fiche de mission formalisée** (objectif, périmètre inclus/exclus,
  livrables, contraintes, échéance).
- Chaque agent rend un **rapport structuré** ; le donneur d'ordre peut demander des corrections
  (trace dans `journal.md`).

## 4. Contrôles et validations humaines

- **Validation humaine obligatoire** pour : périmètre, exigences validées, décisions techniques (ADR),
  planning, recette, toute clôture de question client.
- **Autorisé sans validation préalable** : rapports brouillons, questions ouvertes, recommandations 🟩,
  corrections de forme (voir `AGENTS.md` §11).
- Marquage systématique 🟦 fait / 🟨 hypothèse / 🟩 recommandation (`AGENTS.md` §10 DoD).

## 5. Gestion des erreurs et des désaccords

1. Chaque agent documente sa position et ses arguments.
2. L'Orchestrator confronte les positions, identifie le point de désaccord exact.
3. Consensus → consigné ; sinon **escalade au chef de projet humain** (`AGENTS.md` §7).
4. Les contradictions sont **documentées, jamais effacées** (ex. : audit `docs/analyse/07`, `11`).
5. Erreurs de production (futures) : rapport de défaut avec gravité Bloquant/Majeur/Mineur (QA).

## 6. Phases du projet et gates de validation

Analyse (🟢 validée J-007) → Réunion client (Q1–Q14) → Architecture (ADR) → Plan → Développement
(⛔ interdit avant validations) → Tests → Recette → Déploiement.
