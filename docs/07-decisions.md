# 07 — Registre des décisions (ADR)

**Projet :** Chez Mama Rita
**Statut :** 🟡 Registre ouvert — **aucune décision enregistrée à ce jour**
**Dernière mise à jour :** 2026-11-04

> Règle : toute décision importante (périmètre, architecture, technologie, planning, règle métier)
> doit être tracée ici via une fiche ADR (`templates/decision-record.md`), **validée par le chef
> de projet humain**. Aucun agent ne valide seul.

## Décisions en attente (dépendent des questions ouvertes)

| ID | Sujet | Dépend de | Statut |
|----|-------|-----------|--------|
| D-01 | Règle de paiement (servie vs prête) | Q2 | 🔴 En attente du client |
| D-02 | Mode de facture (impression vs PDF) | Q3 | 🔴 En attente du client |
| D-03 | Frontière « disponibilité » / stocks | Q4 | 🔴 En attente du client |
| D-04 | Durée de conservation des données | Q5 | 🔴 En attente du client |
| D-05 | Choix d'architecture et de stack | Q1, Q6, Q14 + validation phase analyse | 🔴 Non tranché |
| D-06 | Politique de sauvegarde | Q12 | 🔴 En attente du client |
| D-07 | Stratégie de recette et mode formation | Q13 | 🔴 En attente du client |
| D-08 | Règles d'annulation de commande | Q10 | 🔴 En attente du client |

## ADR enregistrés

### ADR-D-VAL-01 — Validation de la phase d'analyse métier
- **Date :** 2026-11-04 · **Statut :** 🟢 Validé le 2026-11-04 par le chef de projet humain
- **Décision :** la phase d'analyse métier est validée comme stable (documents `docs/analyse/10`
  version corrigée, `11`, `12`, `13` — verdict MISSION 05 : VALIDÉ).
- **Portée et limites :** cette validation **ne clôture aucune question client** (Q1–Q14, SQ-A…SQ-E
  restent 🔴 ouvertes) et **n'autorise ni l'architecture définitive ni le développement**.
- **Conséquences :** prochaine étape = réunion client pour les réponses Q1–Q14/SQ-A…SQ-E (SQ-A
  prioritaire), puis revue d'architecture avec ADR.

---

<!-- Format d'une fiche ADR (à copier, modèle dans templates/decision-record.md) :
### ADR-XXX — Titre
- **Date :** …  **Statut :** Proposé / Validé / Rejeté  **Décideur :** Chef de projet
- **Contexte :** …  **Options :** …  **Décision :** …  **Conséquences :** …
-->
