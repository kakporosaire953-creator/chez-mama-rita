# Synthèse de l'Orchestrator — comparaison des analyses et questions au client

**Projet :** Chez Mama Rita — phase d'analyse du besoin
**Date :** 2026-11-04
**Sources comparées :** rapports des agents 01 (Métier), 02 (Architecture), 03 (UX), 04 (Domaine restauration), 05 (Qualité), 06 (Sécurité/DevOps)

---

## 1. Points d'accord (consensus des 6 agents)

| # | Point d'accord | Agents concernés |
|---|----------------|------------------|
| A1 | Le problème cœur est la **fiabilité de la chaîne commande → cuisine → caisse → paiement**, pas l'informatisation en soi | Tous |
| A2 | Les 4 acteurs (Serveur, Cuisinier, Caissier, Gérant) et leurs responsabilités sont cohérents | Tous |
| A3 | La **transmission temps réel à la cuisine** et le **suivi des statuts** sont les fonctionnalités les plus critiques | 01, 02, 03, 05 |
| A4 | La **facturation doit être 100 % automatique** (zéro erreur de calcul, rendu de monnaie) | 01, 04, 05 |
| A5 | L'application doit fonctionner **sans dépendre d'Internet** (contexte Cotonou) | 02, 06 |
| A6 | Les 4 exclusions du brief (paiement en ligne, stocks, fidélité, multi-site) sont claires et respectées | Tous |
| A7 | L'adoption par les serveurs est le risque n°1 : si l'appli est plus lente que le papier, elle sera contournée | 01, 03 |
| A8 | Sauvegarde + restauration testée sont indispensables (données financières) | 02, 05, 06 |
| A9 | Contrôle d'accès par rôle + journal des actions sensibles | 02, 06 |

## 2. Points de désaccord / tensions entre agents

| # | Sujet | Positions | Statut |
|---|-------|-----------|--------|
| D1 | Moment du paiement | Doc 02 propose « paiement après servie » ; l'agent 04 note que certains restaurants encaissent dès « prête » | 🔴 **Ouvert — question client (Q2)** |
| D2 | Stack technique | Doc 03 propose PostgreSQL + PWA + WebSocket ; agent 02 rappelle qu'une alternative plus légère (SQLite) doit être comparée et qu'**aucune décision n'est prise** | 🟡 Proposition non validée — sera tranchée en revue d'architecture, pas maintenant |
| D3 | Matériel | Doc 03 suppose des tablettes ; agent 03 souligne que le matériel réel est inconnu | 🟡 Hypothèse à vérifier (Q1) |
| D4 | Impression | Doc 02 prévoit impression/PDF ; agent 04 demande si une imprimante ticket existe | 🔴 **Ouvert — question client (Q3)** |

## 3. Contradictions identifiées (à résoudre explicitement)

| # | Contradiction | Explication | Où la résoudre |
|---|---------------|-------------|----------------|
| C1 | **« Gestion des disponibilités » vs « pas de gestion des stocks »** | Marquer un plat indisponible est une forme manuelle de suivi de stock, pourtant exclue du périmètre. La frontière doit être explicitée : V1 = rupture **manuelle** déclarée par le gérant, pas de décrément automatique de stock | Doc 01/02 à préciser + Q4 |
| C2 | **« Factures simples » vs conservation de l'historique** | Le brief demande des factures simples ET un tableau de bord sur les ventes passées : il faut définir la durée de conservation des données | Q5 |
| C3 | **Doc 03 traite des choix techno comme acquis** | L'architecture (PostgreSQL, WebSocket…) y est présentée comme « proposée », mais le présent exercice interdit toute décision technique définitive en phase d'analyse | Doc 03 annoté (voir §8 de l'agent 02) ; décisions en ADR plus tard |

## 4. Faits / hypothèses / recommandations — bilan global

- 🟦 **Faits** : flux papier + oral, erreurs de facturation, 4 acteurs, 6 fonctionnalités, 4 exclusions, mono-restaurant à Cotonou.
- 🟨 **Hypothèses à vérifier** : instabilité Internet, matériel (tablettes/PC), coupures de courant, TVA/mentions légales, conservation des données,Comfort numérique de l'équipe.
- 🟩 **Recommandations convergentes** : serveur local autonome, rôles stricts, journal d'audit, sauvegardes testées, écrans adaptés aux 3 contextes (salle/cuisine/caisse).

## 5. Liste consolidée des questions pour le chef de projet / client

Avant de passer à la conception, le chef de projet doit obtenir des réponses à :

1. **Q1 — Matériel** : quels appareils existent déjà (tablettes, PC, écran cuisine, imprimante) et quelles tailles d'écran ? Y a-t-il un Wi-Fi fiable et un endroit verrouillable pour le poste serveur ?
2. **Q2 — Règle de paiement** : encaissement autorisé dès « prête » ou seulement après « servie » ?
3. **Q3 — Impression** : faut-il imprimer les tickets (imprimante disponible ?) ou générer des PDF ?
4. **Q4 — Frontière stocks** : la « disponibilité » se limite-t-elle à une déclaration manuelle de rupture par le gérant (pas de stock décrémenté automatiquement) ?
5. **Q5 — Conservation** : combien de temps conserve-t-on commandes et factures (obligation légale béninoise) ?
6. **Q6 — Taille du restaurant** : nombre de tables, couverts, serveurs par service, volume de commandes en pic de midi ?
7. **Q7 — Encaissement actuel** : espèces uniquement, ou aussi carte/virement manuel traité hors appli ?
8. **Q8 — Facture** : y a-t-il des mentions obligatoires (TVA, adresse, n° d'identification fiscale) ? Faut-il pouvoir découper l'addition par personne (split bill) ?
9. **Q9 — Menu** : existe-t-il des menus du jour, « demies », suppléments facturés à part, ou un plat du jour changeant ?
10. **Q10 — Annulations** : qui peut annuler une commande, à quel stade, et faut-il un motif obligatoire ?
11. **Q11 — Admin** : qui crée/désactive les comptes (le gérant ?) et quelle procédure en cas de départ d'un employé ?
12. **Q12 — Sauvegarde** : quel support de sauvegarde est disponible sur place (clé USB, disque externe, NAS) ?
13. **Q13 — Recette** : qui exécute et signe la recette côté client ? Faut-il un mode « formation » avec données fictives ?
14. **Q14 — Indisponibilité** : quel temps d'arrêt maximum est acceptable en plein service ?

---

**Décision de l'Orchestrator :** la phase d'analyse est **complète mais non close**. Les brouillons de cadrage (désormais dans `docs/brouillons/`) restent non validés. **Aucune conception détaillée ni aucun code ne démarrera avant (a) les réponses aux questions Q1–Q14 et (b) la validation humaine explicite de cette synthèse.**
