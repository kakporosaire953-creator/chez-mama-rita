# 12 — MISSION 04 : Rapport de corrections et d'assainissement de l'analyse métier

**Date :** 2026-11-04
**Document corrigé :** `docs/analyse/10-analyse-approfondie-besoin-metier.md` (seul fichier modifié)
**Audit de référence :** `docs/analyse/11-audit-rapport-analyse-metier.md` (verdict : Acceptable sous réserves)
**Statut :** 🟡 En attente de validation du chef de projet

---

## 1. Anomalies corrigées

| Anomalie | Gravité | Correction appliquée dans le rapport 10 |
|----------|---------|------------------------------------------|
| F-01 | 🟠 Majeur | Origine de chaque EF-01…EF-29 classée (🟦 Direct / 🟨 Impliqué / 🟩 Proposé) avec précision par exigence |
| F-02 | 🟠 Majeur | Origine de chaque UC-01…UC-11 classée ; affirmation « les 6 familles couvrent UC-01…UC-08 » **corrigée** : UC-09/10/11 = 🟩 propositions |
| F-03 | 🟡 Mineur | Doublon UC-01/EX-01 supprimé (renvoi croisé) |
| F-04 | 🟡 Mineur | « Factures simples » : ce qui est exclu (taxes, avoir, numérotation) listé comme dépendant de Q3/Q8/SQ-A |
| F-05 | 🟡 Mineur | Précondition UC-07 « après servie » explicitement marquée 🟩 Q2 non validée |
| F-06 | 🟡 Mineur | Flux TO-BE et statuts marqués 🟩 (Q2) partout où utilisés |
| F-07 | 🟡 Mineur | Clôture journalière de caisse examinée §6 → classée 🟩 proposition (candidate UC-12), **non intégrée** |
| F-08 | 🟡 Mineur | Scénario concurrence (2 serveurs, même table) ajouté §6 → 🟩 scénario QA (ENF-08), **non intégré comme exigence** |
| F-09 | 🟡 Mineur | Sauvegarde/restauration examinée §6 → 🟩 recommandation technique (ENF, Q12), **non intégrée comme UC** |
| F-10 | 🟡 Mineur | Impression ticket cuisine examinée §6 → 🟩 proposition liée Q3 |
| F-11 | 🟡 Mineur | Matrice de permissions marquée « 🟩 proposée — à valider (Q11) » |

## 2. Exigences reclassées (F-01)

- 🟦 **Direct (12)** : EF-01, 02, 04, 08, 09, 11, 13, 14, 15, 18, 23, 25
- 🟨 **Impliqué (9)** : EF-06, 07, 10, 16, 19, 20, 22, 24, 27
- 🟩 **Proposé (8)** : EF-03, 05, 12, 17, 21, 26, 28, 29
- ENF : 🟨 ENF-01, 02, 03, 04, 08, 10 · 🟩 ENF-05, 06, 07, 09 (ENF-02 : la valeur « 3 s » reste 🟨, à confirmer via Q14/Q6)
- **UC** : 🟦 UC-01, 03, 04, 05, 07, 08 · 🟨 UC-02, 06 · 🟩 UC-09, 10, 11

## 3. Éléments supprimés ou fusionnés (et pourquoi)

- Affirmation erronée « les 6 familles du brief couvrent UC-01…UC-08 » → remplacée par la
  traçabilité correcte (justification : F-02, incohérence interne).
- Doublon entre UC-01 et EX-01 sur la disponibilité des plats → fusionné en renvoi croisé
  (justification : F-03, redondance).
- Aucun élément métier important supprimé ; toutes les suppressions sont des **redondances**,
  justifiées ci-dessus.

## 4. Propositions conservées en attente de validation client (🟩)

EF-03, 05, 12, 17, 21, 26, 28, 29 · UC-09, 10, 11 · clôture journalière de caisse (UC-12
candidate) · impression ticket cuisine · commandes complémentaires/même table · split bill (Q8) ·
suppléments/menus du jour/demies (Q9) · moyens de paiement multiples (Q7) · paiement anticipé (Q2/SQ-E) ·
MECeF (SQ-A) · rétention 10 ans (Q5/SQ-C) · mode formation (Q13) · reprise ≤ 5 min (Q14) ·
sauvegarde multi-niveaux (Q12) · matrice de permissions (Q11).

## 5. Anomalies non corrigibles faute d'informations (restent ouvertes)

- Valeur mesurable du délai de transmission cuisine (ENF-02 « 3 s ») → dépend de Q14/Q6.
- Moyens de paiement définitifs (EF-19) → Q7/SQ-D.
- Format de facture (ticket/PDF/MECeF) → Q3/SQ-A.
- Durée de conservation (ENF-07) → Q5/SQ-C.
- Nombre de salles/tables/volumétrie → Q1/Q6/SQ-B.

## 6. Fichiers modifiés et créés

| Fichier | Action |
|---------|--------|
| `docs/analyse/10-analyse-approfondie-besoin-metier.md` | ✅ Modifié (corrections F-01…F-11, origines, §6 classification) |
| `docs/analyse/12-rapport-corrections-mission-04.md` | ✅ Créé (ce rapport) |
| Tous les autres fichiers | ❌ Non modifiés |

## 7. Vérification finale (critères de validation MISSION 04)

| Critère | Résultat |
|---------|----------|
| Aucune proposition présentée comme exigence confirmée | ✅ (origines 🟦/🟨/🟩 sur chaque EF et UC) |
| Chaque exigence a une origine identifiable | ✅ (§3 du rapport 10) |
| UC cohérents avec les besoins identifiés | ✅ (UC 🟦/🟨 issus du brief ; 🟩 marqués) |
| Aucune question client résolue artificiellement | ✅ (Q1–Q14 + SQ-A…SQ-E toujours ouvertes) |
| Contradictions majeures corrigées | ✅ (F-01, F-02) |
| Fidélité au périmètre | ✅ (4 exclusions intactes ; ajouts = 🟩 uniquement) |
| Pas de développement / pas de technologie | ✅ |

⏸️ **MISSION 04 terminée — en attente de votre validation avant toute nouvelle mission.**
