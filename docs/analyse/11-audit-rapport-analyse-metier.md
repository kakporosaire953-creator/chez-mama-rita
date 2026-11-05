# 11 — MISSION 03 : Audit et validation du rapport d'analyse métier

**Document audité :** `docs/analyse/10-analyse-approfondie-besoin-metier.md`
**Date :** 2026-11-04
**Auditeurs :** Business Analyst, QA & Testing, Security Auditor, Software Architect, Critical Reviewer
**Consolidation :** Orchestrator
**Contraintes respectées :** aucun fichier existant modifié ; aucune décision métier inventée ;
Q1–Q14 et SQ-A…SQ-E restent ouvertes ; pas d'architecture définitive ; pas de développement.

---

## 0. Verdict de l'Orchestrator (résumé)

> ### 🟡 **ACCEPTABLE SOUS RÉSERVES**
>
> Le rapport est globalement solide (structure complète, séparation 🟦/🟨/🟩 respectée,
> questions ouvertes préservées). Il comporte toutefois **2 problèmes majeurs** et plusieurs
> mineurs à corriger avant validation métier. Aucun problème bloquant.

| Gravité | Nombre | Définition |
|---------|--------|------------|
| 🔴 Bloquant | 0 | Empêche la validation |
| 🟠 Majeur | 2 | Doit être corrigé avant validation (F-01, F-02) |
| 🟡 Mineur | 9 | À corriger ou clarifier (F-03…F-11) |

---

## 1. Points conformes ✅

1. **Séparation faits/hypothèses/recommandations** globalement respectée (🟦/🟨/🟩) — vérifié par BA et Critical Reviewer.
2. **« Trois salles » correctement rétrogradé en hypothèse 🟨** (proposition Q1 non confirmée).
3. **14 questions ouvertes conservées**, aucune clôturée — conforme à AGENTS.md §9.
4. Structure conforme au livrable demandé (acteurs, processus, flux, exigences, UC, exceptions, questions, recommandations).
5. Flux AS-IS strictement fondés sur les faits du brief (papier, oral, erreurs de facturation) — aucun fonctionnement inventé.
6. Exceptions EX-01…EX-08 et risques R-OP1…3 pertinents et cohérents avec les propositions documentées.
7. Aucune technologie choisie ; l'architecture reste hors scope du rapport — conforme.
8. Traçabilité vers les sources (brief, docs/01, brouillons, analyse 01–09) présente.

## 2. Erreurs et incohérences détectées

| ID | Gravité | Problème | Détecté par |
|----|---------|----------|-------------|
| F-01 | 🟠 Majeur | **Traçabilité incomplète** : le §4.1 présente EF-01…29 comme « ancrés dans le brief », mais plusieurs EF du brouillon vont **au-delà** du brief (ex. EF-03 archiver, EF-21 réimprimer une facture, EF-26 ventes par serveur, EF-29 journal des actions) — ce sont des **propositions dérivées**, pas des faits du brief | BA / Critical Reviewer |
| F-02 | 🟠 Majeur | **Incohérence interne** : le §8.3 point 6 affirme que « les 6 familles du brief couvrent les UC-01…UC-08 », mais **UC-09 (comptes), UC-10 (annulation), UC-11 (mode formation)** ne viennent ni du brief ni de UC-01…08 — ils viennent du brouillon EF-27…29 et des propositions 🟩. Formulation à corriger | Critical Reviewer |
| F-03 | 🟡 Mineur | Redondance : disponibilité des plats apparaît à la fois dans UC-01 et EX-01 sans renvoi croisé clair | BA |
| F-04 | 🟡 Mineur | « Factures simples » (brief) reste non défini ; le rapport ne liste pas ce que « simple » exclut (taxes ? avoir ? numérotation ?) | BA |
| F-05 | 🟡 Mineur | UC-07 précondition « commande servie » vient de la proposition Q2 🟩 — elle est présentée comme une règle alors qu'elle n'est pas validée | Critical Reviewer |
| F-06 | 🟡 Mineur | Le §3 TO-BE intègre les statuts « Reçue → … → Payée » sans rappeler partout que c'est 🟩 (Q2) | Critical Reviewer |
| F-07 | 🟡 Mineur | Pas de cas d'utilisation pour la **clôture de journée / caisse** (rapport Z, total encaissé vs attendu) alors que la mission citait « clôture » | QA / Critical Reviewer |
| F-08 | 🟡 Mineur | Scénario « deux serveurs sur la même table simultanément » absent (seul le double-clic EX-04 est couvert) | QA |
| F-09 | 🟡 Mineur | Scénario **sauvegarde/restauration** absent de la liste des UC (présent seulement en risque R-OP3) | QA |
| F-10 | 🟡 Mineur | Impression du ticket cuisine (Q3) n'apparaît dans aucun UC | QA |
| F-11 | 🟡 Mineur | Matrice de permissions (§8.2) présentée sans statut « proposée/à valider » explicite | Security Auditor |

## 3. Exigences à reformuler

| Exigence concernée | Problème | Reformulation proposée |
|--------------------|----------|------------------------|
| Famille « Paiements et factures simples » (EF-18…22) | « simple » ambigu + conflit avec proposition Q7 (multi-moyens) et Q3 (MECeF) | « Facturation automatique de l'addition d'une table, avec encaissement au moins en espèces ; moyens supplémentaires et format fiscal selon réponses Q3/Q7/Q8/SQ-A » |
| EF-04 / UC-01 disponibilité | Workflow gérant-vs-cuisine non tranché (Q4) | « Le gérant peut marquer un plat indisponible ; le responsable cuisine peut signaler une rupture (proposition Q4, à valider) » |
| EF-13 délai de transmission | « automatique » sans critère mesurable | « La commande envoyée apparaît sur l'écran cuisine en moins de X secondes (X = à fixer, lié à Q14) » |
| EF-19 encaissement | « espèces » (brouillon) vs « multi-moyens manuel » (Q7 🟩) | Suspendre la rédaction définitive jusqu'à la réponse client Q7/SQ-D |
| UC-07 précondition | Règle Q2 non validée | « Encaissement autorisé selon la règle validée par le client (Q2 : après « servie » ou dès « prête ») » |

## 4. Informations manquantes

1. **Clôture de journée / rapport de caisse** (total du jour, écarts) — aucune UC ni exigence.
2. **Impression ticket cuisine** (Q3) — absent des UC.
3. **Concurrence d'accès** (2 serveurs, même table) — absent.
4. **Sauvegarde/restauration** en tant que fonction testable (UC) — seulement un risque.
5. **Régime fiscal exact** du restaurant (assujetti MECeF ? TVA ?) — SQ-A, bloquant pour la facturation.
6. **Volumétrie réelle** (Q6) — bloque le dimensionnement des critères de performance.
7. **Nombre de salles/tables/serveurs** (Q1/Q6/SQ-B).
8. **Durée de conservation validée** (Q5/SQ-C) — bloque l'archivage.
9. **Qui valide la recette** et sous quelle forme (Q13).
10. **Définition de «disponibilité»** (manuelle vs automatique) — Q4.

## 5. Risques critiques identifiés par l'audit

| Risque | Pourquoi critique | Parade |
|--------|-------------------|--------|
| RK-1 : Des propositions 🟩 (statuts, Q2, multi-moyens, MECeF…) pourraient être traitées comme validées en aval | Casserait la règle « aucune exigence inventée » | Verdict « sous réserves » + corrections F-01/F-02/F-05/F-06 obligatoires avant diffusion |
| RK-2 : Facturation non conforme (MECeF) si le régime fiscal est mal évalué | Risque légal/sanctions pour le restaurant | SQ-A à traiter en priorité à la réunion client |
| RK-3 : Exigences non testables faute de critères mesurables | QA bloqué, recette impossible | QA ajoute les critères d'acceptation après validation client |
| RK-4 : Scénarios opérationnels oubliés (clôture de caisse, panne, concurrence) | Produit incomplet en conditions réelles | Ajouter UC-12 (clôture de journée), UC-13 (sauvegarde/restauration), scénario concurrence |
| RK-5 : Permissions non formalisées | Risque fraude/accès non autorisé | Valider la matrice rôles × actions (Q11) + journal d'audit |

## 6. Corrections recommandées (à appliquer après validation du chef de projet)

1. **F-01** : dans `docs/analyse/10`, distinguer « EF issus du brief » vs « EF dérivés/proposés » (ex. EF-03, EF-21, EF-26, EF-29 → statut 🟩).
2. **F-02** : corriger le §8.3 point 6 — UC-09/10/11 proviennent du brouillon/propositions, pas du brief.
3. **F-05/F-06** : marquer explicitement 🟩 partout où une règle Q2/Q14 est utilisée comme si elle était actée.
4. **F-07…F-10** : ajouter UC-12 clôture de journée, UC-13 sauvegarde/restauration, scénario concurrence même table, ticket cuisine (Q3).
5. **F-11** : marquer la matrice de permissions « 🟩 proposée — à valider (Q11) ».
6. Reformuler les exigences du §3 selon les 5 lignes proposées.
7. Ajouter SQ-A en **prioritaire** à l'agenda client (risque RK-2).

## 7. Verdict détaillé par agent

| Agent | Verdict | Justification |
|-------|---------|---------------|
| Business Analyst | Acceptable sous réserves | Traçabilité à compléter (F-01), ambiguïtés à lever (F-04) |
| QA & Testing | Acceptable sous réserves | Critères mesurables manquants ; UC-12/13 + concurrence + ticket cuisine à ajouter |
| Security Auditor | Acceptable sous réserves | Matrice de permissions à marquer « proposée » ; audit des opérations sensibles OK |
| Software Architect | Acceptable | Contraintes futures bien identifiées (temps réel, hors-ligne, fiscal, rétention, volumétrie) sans proposer d'architecture |
| Critical Reviewer | Acceptable sous réserves | F-02 incohérence interne à corriger ; sinon propositions bien distinguées des faits |
| **Orchestrator** | 🟡 **ACCEPTABLE SOUS RÉSERVES** | 0 bloquant, 2 majeurs (F-01, F-02), 9 mineurs ; corrections listées au §6 |

---

⏸️ **Audit terminé.** Aucune décision métier inventée ; Q1–Q14 et SQ-A…SQ-E restent ouvertes ;
aucun fichier existant modifié ; pas d'architecture définitive ; pas de développement.
**En attente de la validation du chef de projet** (notamment pour appliquer les corrections §6
sur `docs/analyse/10`).
