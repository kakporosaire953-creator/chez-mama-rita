# TC-ENCAISSEMENT — Paiement et facturation

**Statut :** 📝 Préparé — **non exécuté** (aucun code développé)
**Fonctionnalité :** paiements et factures simples (UC-07 / EF-18 à EF-22)

| Champ | Valeur |
|-------|--------|
| ID | TC-ENCAISSEMENT-01 |
| Préconditions | Commande servie (statut selon règle validée 🟩 Q2) ; compte Caissier actif |
| Étapes | 1. Ouvrir la facture de la table (3 plats, quantités variées) · 2. Vérifier le total calculé automatiquement · 3. Saisir « montant reçu = 25 000 XOF » pour une facture de 20 500 XOF · 4. Valider l'encaissement · 5. Vérifier facture n° unique + clôture de table |
| Résultat attendu | 2. Total exact, zéro erreur (entiers XOF) · 3. Rendu = 4 500 XOF · 4. Facture créée, commande « payée » · 5. Table redevenue libre ; facture consultable/réimprimable (🟩 EF-21) ; format selon réponses Q3/SQ-A (MECeF) |
| Origine | Brief 🟦 (famille 5) ; espèces = 🟨 (Q7) ; MECeF = 🟩 SQ-A |
