# TC-STATUTS — Suivi des statuts des commandes

**Statut :** 📝 Préparé — **non exécuté** (aucun code développé)
**Fonctionnalité :** suivi des statuts (UC-05, UC-06 / EF-14, 15, 16)

| Champ | Valeur |
|-------|--------|
| ID | TC-STATUTS-01 |
| Préconditions | Une commande présente en cuisine |
| Étapes | 1. Cuisinier passe la commande « En préparation » · 2. Puis « Prête » · 3. Vérifier la visibilité temps réel côté serveur · 4. Serveur marque « Servie » · 5. Vérifier les horodatages de chaque transition |
| Résultat attendu | Chaque statut est daté et visible des bons acteurs en temps réel ; la séquence suivie est celle validée par le client (🟩 Q2 : Reçue → En préparation → Prête → Servie → Payée) |
| Origine | Brief 🟦 (famille 4) ; liste exacte des statuts = 🟩 Q2 |
