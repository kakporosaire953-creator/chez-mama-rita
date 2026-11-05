# 04 — Plan de travail et organisation de l'équipe

**Projet :** Chez Mama Rita
**Date :** 2026-11-04
**Statut :** Brouillon à valider

## 1. Principe directeur

Aucun développement ne démarre avant la **validation** des documents 01 à 03 et du plan de tests (document 05).
Ensuite, travail en **sprints de 2 semaines**, avec revue et démo à chaque fin de sprint.

## 2. Phases du projet

| Phase | Contenu | Durée estimée | Sortie |
|-------|---------|---------------|--------|
| **Phase 0 — Cadrage** (en cours) | Vision, besoins, exigences, architecture, plan de tests | 1 semaine | Documents 01–05 validés par le client |
| **Phase 1 — Socle technique** | Projet initialisé, base de données, authentification + rôles, déploiement local (Docker) | 2 semaines (Sprint 1) | Login fonctionnel, rôles, base déployable sur le mini-PC |
| **Phase 2 — Cœur métier : menu + commandes** | Gestion du menu, tables, prise de commande, transmission cuisine temps réel, statuts | 4 semaines (Sprints 2–3) | Un serveur peut prendre une commande, la cuisine la voit et la marque prête |
| **Phase 3 — Caisse et factures** | Facturation, encaissement espèces + rendu, impression/PDF, clôture de table | 2 semaines (Sprint 4) | Encaissement complet et fiable |
| **Phase 4 — Tableau de bord** | Ventes du jour/période, top plats, ventes par catégorie et serveur | 2 semaines (Sprint 5) | Dashboard consultable par le gérant |
| **Phase 5 — Recette, déploiement, formation** | Tests de recette avec le client, corrections, installation sur site, formation des 4 profils, sauvegardes | 2 semaines (Sprint 6) | Application en production au restaurant, utilisateurs formés |

**Durée totale estimée : ~13 semaines (3 mois) après validation du cadrage.**

## 3. Organisation en « équipe d'agents spécialisés »

| Rôle | Responsabilité dans ce projet |
|------|------------------------------|
| **Chef de projet / PO** | Validation des documents, priorisation, recette avec le client |
| **Analyste (BA)** | Documents 01–02 (besoins, exigences), maquettes d'écrans |
| **Architecte** | Document 03, revue des décisions techniques, ADR |
| **Dev Back-end** | API, base de données, WebSocket, factures PDF, sécurité |
| **Dev Front-end** | Écrans tablette serveur, écran cuisine, caisse, dashboard (responsive) |
| **QA / Testeur** | Document 05, exécution des tests, rapport de bugs, recette |
| **DevOps** | Docker, déploiement local, sauvegardes, procédure de restauration |

## 4. Rituels

- **Revue de cadrage (J0+1 semaine)** : validation des documents 01–05 avec le gérant.
- **Daily court (15 min)** en sprint : avancement, blocages.
- **Revue de sprint (fin de sprint)** : démo des fonctionnalités livrées.
- **Rétrospective** : amélioration continue du processus.
- **Recette finale** : scénarios utilisateur réels avec serveurs, cuisinier, caissier et gérant.

## 5. Livrables attendus en fin de projet

1. Application déployée et fonctionnelle au restaurant (serveur local).
2. Code source versionné + documentation technique (README, `docs/adr/`).
3. Guide utilisateur par rôle (1 page par profil).
4. Procédure de sauvegarde / restauration.
5. Rapport de recette signé par le gérant.

## 6. Risques principaux et parades

| Risque | Probabilité | Parade |
|--------|-------------|--------|
| Connexion Internet instable sur site | Élevée | Serveur local + PWA (ENF-01), test de fonctionnement hors-ligne |
| Résistance au changement des serveurs | Moyenne | Formation courte, écrans simples, période de transition papier/appli |
| Panne du mini-PC serveur | Faible | Sauvegardes quotidiennes + procédure de restauration testée (ENF-06) |
| Écran cuisine illisible (graisse, chaleur) | Moyenne | Tablette dédiée protégée, grands caractères, contraste élevé |
| Dérive du périmètre (stocks, fidélité demandés en cours de route) | Moyenne | Périmètre V1 figé (document 01 §5), évolutions notées pour une V2 |

---

*Plan à valider avec le client avant le démarrage du Sprint 1.*
