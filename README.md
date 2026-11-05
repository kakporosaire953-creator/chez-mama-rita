# Chez Mama Rita — Gestion numérique du restaurant

Solution de gestion numérique pour le restaurant **Chez Mama Rita**, situé à **Cotonou, Bénin**.

## 🎯 Objectif du projet

Remplacer le système manuel (commandes sur papier, transmission orale à la cuisine, facturation manuelle)
par une application permettant de :

- gérer les plats, prix et disponibilités ;
- prendre les commandes par table ;
- transmettre automatiquement les commandes à la cuisine ;
- suivre les statuts des commandes ;
- gérer les paiements et factures simples ;
- consulter un tableau de bord des ventes et des plats les plus commandés.

**Hors périmètre V1 :** paiement mobile en ligne, gestion des stocks, programme de fidélité, multi-restaurant.

> ⚠️ Ce contexte est un **point de départ à vérifier** avec le client avant d'être considéré comme définitif.

## 📁 Organisation des dossiers

| Dossier / fichier | Rôle |
|-------------------|------|
| `AGENTS.md` | Règles générales de collaboration applicables à tous les agents IA |
| `agents/` | Profil et instructions de chaque agent spécialisé (7 agents) |
| `docs/` | Documents de travail du projet (contexte, exigences, workflow, architecture, planning, tests, décisions) |
| `docs/analyse/` | Rapports d'analyse préliminaire des spécialistes + synthèse Orchestrator + test MISSION 01 + recommandations « contexte béninois » |
| `docs/brouillons/` | Anciens brouillons de cadrage (contenu préservé, non validés) |
| `templates/` | Modèles réutilisables (mission, rapport d'analyse, fiche de décision, compte-rendu) |
| `journal.md` | Journal chronologique des missions, échanges, corrections et décisions |
| `CHANGELOG.md` | Suivi des évolutions validées de la documentation |
| `tests/` | Stratégie et futurs cas de tests (aucun code applicatif pour le moment) |

## 🤝 Méthode de travail

Le projet est mené par une **équipe de 7 agents IA spécialisés**, coordonnés par un Orchestrator,
selon les règles définies dans `AGENTS.md` :

1. **Le chef de projet humain conserve l'autorité finale** — aucun agent ne valide seul une décision importante.
2. Les agents distinguent toujours **faits**, **hypothèses** et **recommandations**.
3. **Aucune exigence n'est inventée** ; les informations manquantes sont signalées comme questions ouvertes.
4. Les contradictions entre agents sont **documentées**, pas ignorées.
5. Toute modification importante est **traçable** (journal + changelog + fiches de décision dans `docs/07-decisions.md`).
6. **Aucun développement ne démarre** avant validation humaine des phases d'analyse, d'architecture, de planification et de tests.

## 🚀 Comment lancer le workflow des agents

1. **Lire `AGENTS.md`** (règles communes) puis le profil de l'agent concerné dans `agents/`.
2. **L'Orchestrator attribue la mission** via le modèle `templates/agent-mission.md` et l'inscrit dans `journal.md`.
3. **L'agent produit son rapport** selon `templates/analysis-report.md` (faits 🟦 / hypothèses 🟨 / recommandations 🟩).
4. **Le Critical Reviewer relit**, l'Orchestrator consolide et fait valider par le **chef de projet humain**.
5. **La décision/validation est enregistrée** dans `journal.md`, `CHANGELOG.md` et `docs/07-decisions.md` (ADR).
6. **Règles absolues :** aucune décision importante sans validation humaine ; aucune exigence inventée ;
   aucune question client clôturée sans réponse écrite ; **aucun développement** avant validation des phases préalables.

## 📌 État actuel du projet

- **Phase en cours :** analyse du besoin (ouverte — en attente de validation humaine).
- **14 questions ouvertes (Q1–Q14)** en attente de clarification auprès du client — voir `docs/02-requirements.md` § « Questions ouvertes ».
- Aucun code applicatif n'existe. Aucune décision technique définitive n'a été prise.

## ▶️ Prochaine mission proposée

**Analyse approfondie du besoin métier** (mission du Business Analyst Agent, sous coordination de l'Orchestrator),
en intégrant les réponses du client aux questions Q1–Q14 lorsqu'elles seront disponibles.
