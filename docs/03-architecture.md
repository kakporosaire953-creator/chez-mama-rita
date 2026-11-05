# 03 — Architecture (propositions justifiées — aucune décision définitive)

**Projet :** Chez Mama Rita
**Statut :** 🟩 Propositions justifiées, **en attente des réponses client (Q1, Q6, Q14) et de la
validation du chef de projet**. Aucune technologie n'est choisie arbitrairement : chaque option
est justifiée ci-dessous ; la décision sera enregistrée en ADR dans `docs/07-decisions.md`.
**Mise à jour :** 2026-11-04 (MISSION 06 — conformité énoncé).

> ⚠️ Règle du projet : pas de décision technique définitive avant les réponses client.
> Ce document présente des **options comparées et justifiées**, pas un choix acté.

## 1. Contraintes connues (issues du brief et des propositions 🟩)

🟦 Mono-établissement (pas de multi-restaurant) · 🟦 Pas de paiement en ligne en V1
🟩 (Q1) Réutiliser le matériel existant, Wi-Fi interne, secours électrique, pas de serveur physique imposé
🟩 (Q14) Fonctionnement hors Internet, reprise ≤ 5 min, procédure papier dégradée
🟩 (Q12) Sauvegardes multi-niveaux · 🟩 (Q5/SQ-A) Rétention comptable + facture possiblement conforme MECeF

## 2. Options d'architecture comparées (justifiées)

| Critère | Option A — Mini-PC local + PostgreSQL + appli web (PWA) | Option B — PC existant + SQLite + appli web | Option C — Cloud hybride |
|---------|----------------------------------------------------------|--------------------------------------------|---------------------------|
| Coût | Moyen (achat mini-PC) | **Le plus faible** (réutilise le matériel) | Récurrent (hébergement) |
| Hors-ligne (Q14) | ✅ natif | ✅ natif | ⚠️ nécessite couche locale |
| Fiabilité données (paiements) | ✅ transactions ACID | ✅ ACID, mais moins robuste en multi-poste | ✅ |
| Maintenance | ✅ standard | ✅ simple | ⚠️ dépendance fournisseur |
| Conformité coûts Bénin (CCI 2024 🟩) | 😐 | ✅ | 😐 |
| **Recommandation 🟩** | **Option privilégiée si budget OK** | **Option de secours si budget serré** | À écarter en V1 (coût + dépendance) |

**Raison d'écarter le cloud en V1 :** coûts d'infrastructure élevés au Bénin (contexte CCI 2024) et
exigence de fonctionnement hors Internet (Q14).

## 3. Modèle de données (🟩 proposé — issu du brouillon validé en analyse)

```
UTILISATEUR (id, nom, identifiant, mot_de_passe_haché, rôle, actif)
TABLE (id, numéro, capacité, zone, active)
CATEGORIE (id, nom, ordre)
PLAT (id, nom, description, prix_xof, catégorie_id, disponible, archivé)
COMMANDE (id, table_id, serveur_id, statut, créée_le, servie_le, payée_le, motif_annulation)
LIGNE_COMMANDE (id, commande_id, plat_id, quantité, prix_unitaire, commentaire, statut)
FACTURE (id, numéro, commande_id, caissier_id, total_xof, montant_reçu, rendu, créée_le)
JOURNAL_ACTION (id, utilisateur_id, action, détail, date)
```

Règles : prix figé sur la ligne à la commande ; annulations tracées, jamais supprimées ;
statuts : Reçue → En préparation → Prête → Servie → Payée (🟩 Q2).

## 4. Arborescence cible

**Dépôt (documentation) :**
```
├── README.md · AGENTS.md · journal.md · CHANGELOG.md · LINKEDIN.md
├── agents/ (7 profils) · templates/ (4 modèles)
├── docs/ 01-comprehension … 07-decisions + analyse/ + brouillons/
└── tests/ README + cases/ (6 cas préparés)
```

**Application (cible V1, 🟩) :**
```
app/
├── backend/   (API REST + temps réel + factures PDF + auth par rôle)
├── frontend/  (PWA : écrans serveur / cuisine / caisse / dashboard)
├── db/        (schéma + migrations + sauvegardes)
└── docker/    (déploiement local reproductible)
```

## 5. Raisons motivant les orientations

1. **Local-first** → survie aux coupures Internet/électricité (contexte Cotonou, Q14).
2. **PWA** → un seul code pour tablette serveur, écran cuisine, caisse (Q1, matériel hétérogène).
3. **Temps réel (WebSocket/SSE)** → transmission cuisine < délai fixé (Q14) — mécanisme à confirmer en ADR.
4. **PostgreSQL si mini-PC** → intégrité des paiements ; **SQLite si PC existant** → zéro achat.
5. **Journal d'actions + rôles** → traçabilité exigée par la sécurité (EF-29 🟩, Q11).

## 6. Références

- Propositions détaillées (brouillon) : `docs/brouillons/03-architecture-et-donnees.md`
- Analyse des contraintes : `docs/analyse/02-architecte-systeme.md`, `docs/analyse/09-…`
- Décision future : ADR dans `docs/07-decisions.md` après réponses client.
