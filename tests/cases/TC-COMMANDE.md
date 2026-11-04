# TC-COMMANDE — Prise de commande par table

**Statut :** 📝 Préparé — **non exécuté** (aucun code développé)
**Fonctionnalité :** prise de commandes par table (UC-03 / EF-08, 09, 10)

| Champ | Valeur |
|-------|--------|
| ID | TC-COMMANDE-01 |
| Préconditions | Compte Serveur actif ; table T1 libre ; menu à jour |
| Étapes | 1. Ouvrir une commande sur T1 · 2. Ajouter 2× « Riz au poisson » + 1× « Jus » avec commentaire « sans piment » · 3. Vérifier le total affiché · 4. Modifier une ligne avant envoi · 5. Envoyer en cuisine |
| Résultat attendu | 1. Commande horodatée, rattachée au serveur · 2. Lignes avec quantités/prix · 3. Total = somme exacte (entiers XOF) · 4. Ligne modifiée correctement · 5. Commande transmise (voir TC-CUISINE) |
| Origine | Brief 🟦 (famille 2) ; commentaire = 🟩 (Q9) |
