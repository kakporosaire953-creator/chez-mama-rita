# TC-MENU — Gestion du menu (plats, prix, disponibilités)

**Statut :** 📝 Préparé — **non exécuté** (aucun code développé)
**Fonctionnalité :** gestion des plats, prix et disponibilités (UC-01 / EF-01, 02, 04)

| Champ | Valeur |
|-------|--------|
| ID | TC-MENU-01 |
| Préconditions | Compte Gérant actif ; menu initial chargé |
| Étapes | 1. Créer le plat « Riz au poisson » à 5 000 XOF · 2. Vérifier qu'il apparaît côté serveur · 3. Modifier le prix à 5 500 XOF · 4. Marquer le plat indisponible |
| Résultat attendu | 1. Plat visible immédiatement · 2. Nouvelles commandes à 5 500 XOF, anciennes inchangées · 3. Plat grisé et non sélectionnable |
| Origine | Brief 🟦 (famille 1) ; règle « prix figé » = 🟩 à valider |
