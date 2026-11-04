# 03 — Architecture et modèle de données

**Projet :** Chez Mama Rita
**Date :** 2026-11-04
**Statut :** Proposition à valider

## 1. Vue d'ensemble (architecture 3 tiers, déployée sur place)

```
┌─────────────────────────────────────────────────────────────┐
│                     RÉSEAU LOCAL DU RESTAURANT (Wi-Fi)       │
│                                                             │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────────┐   │
│  │ Tablettes   │   │ Écran cuisine│   │ Poste caisse    │   │
│  │ (serveurs)  │   │ (cuisinier) │   │ (caissier)      │   │
│  │  Navigateur │   │  Navigateur │   │  Navigateur     │   │
│  └──────┬──────┘   └──────┬──────┘   └──────┬──────────┘   │
│         │                 │                  │              │
│         └─────────────────┴──────────────────┘              │
│                           │ HTTP / WebSocket (temps réel)    │
│                    ┌──────┴──────┐                          │
│                    │  SERVEUR    │◄──── mini-PC ou NAS     │
│                    │  LOCAL      │      dans le restaurant  │
│                    │ ┌─────────┐ │                          │
│                    │ │ API REST│ │                          │
│                    │ │+ WebSocket│                         │
│                    │ └────┬────┘ │                          │
│                    │ ┌────┴────┐ │   ┌─────────────┐        │
│                    │ │  Base   │─┼──►│ Sauvegardes │        │
│                    │ │PostgreSQL│  │   │ quotidiennes│        │
│                    │ └─────────┘ │   │  (fichiers) │        │
│                    └─────────────┘   └─────────────┘        │
│                           ▲                                 │
│                    [Internet coupé = appli toujours OK]     │
└─────────────────────────────────────────────────────────────┘
```

**Justification du choix « serveur local » :** à Cotonou, la connexion Internet peut être
instable (ENF-01). Toute l'application tourne donc sur le Wi-Fi local du restaurant ; aucune
dépendance cloud obligatoire. Une sauvegarde externe (clé USB / second poste) reste possible.

## 2. Composants et choix techniques (proposition)

| Couche | Choix proposé | Pourquoi |
|--------|---------------|----------|
| **Interface** | Application web responsive (PWA) en React ou Vue | Une seule base de code pour tablette serveur, écran cuisine et caisse ; fonctionne hors-ligne après premier chargement |
| **API** | Node.js + Express (ou Python + FastAPI) en REST | Écosystème riche, équipe facile à recruter localement |
| **Temps réel** | WebSocket (Socket.IO) ou SSE | Transmission instantanée des commandes à la cuisine (ENF-02) |
| **Base de données** | PostgreSQL | Fiable, transactions ACID (indispensable pour les paiements), sauvegardes natives |
| **Authentification** | Sessions sécurisées ou JWT + rôles (RBAC) | 4 rôles : Serveur, Cuisinier, Caissier, Gérant |
| **Factures** | Génération PDF côté serveur + impression navigateur | Pas de dépendance à une imprimante spécifique |
| **Déploiement** | Docker Compose sur un mini-PC du restaurant | Installation reproductible, sauvegarde = snapshot du volume de données |

*Les choix technologiques définitifs seront confirmés à la revue d'architecture ; l'essentiel est le contrat d'API et le modèle de données ci-dessous.*

## 3. Modèle de données (entités principales)

```
UTILISATEUR (id, nom, identifiant, mot_de_passe_haché, rôle, actif, créé_le)
TABLE (id, numéro, capacité, zone, active)
CATEGORIE (id, nom, ordre)                     -- ex : Entrées, Plats, Boissons
PLAT (id, nom, description, prix_xof, catégorie_id, disponible, archivé, photo_url)
COMMANDE (id, table_id, serveur_id, statut, créée_le, envoyée_le, servie_le, payée_le, annulée_le, motif_annulation)
LIGNE_COMMANDE (id, commande_id, plat_id, quantité, prix_unitaire, commentaire, statut)  -- statut: en attente / en préparation / prêt / servi
FACTURE (id, numéro, commande_id, caissier_id, total_xof, montant_reçu_xof, rendu_xof, créée_le)
JOURNAL_ACTION (id, utilisateur_id, action, détail, date)
```

**Règles métier clés :**
- `prix` est figé sur la `LIGNE_COMMANDE` au moment de la commande (un changement de prix ne modifie pas les commandes passées).
- Une commande ne peut être payée que si toutes ses lignes sont « servies » (ou « prêtes » selon règle métier à confirmer).
- Le `statut` de la commande se déduit des statuts de ses lignes + étapes globales.
- Suppression douce (`archivé`, `annulée_le`) : aucune donnée métier n'est jamais supprimée.

## 4. Flux principaux

### 4.1 Prise de commande → cuisine → service
```
Serveur : ouvre commande table T → ajoute lignes → « Envoyer en cuisine »
   → API crée COMMANDE (statut "envoyée") + LIGNEs (statut "en attente")
   → WebSocket notifie l'écran cuisine (nouvelle commande, sonnerie optionnelle)
Cuisinier : passe la ligne en « préparation » puis « prêt »
   → WebSocket notifie la tablette du serveur (statut temps réel)
Serveur : marque « servie » → la table passe en « à encaisser »
```

### 4.2 Encaissement
```
Caissier : ouvre la table → voit le récapitulatif (lignes + total calculé)
   → saisit montant reçu → système calcule le rendu
   → valide → FACTURE créée (numéro unique), commande "payée", table "libre"
   → impression / affichage du ticket
```

## 5. API REST (aperçu — contrat à figer en revue)

| Méthode | Route | Rôle | Description |
|---------|-------|------|-------------|
| POST | `/api/auth/login` | tous | Connexion, renvoie le token + rôle |
| GET/POST/PUT | `/api/plats`, `/api/plats/:id/disponibilite` | Gérant (écriture), tous (lecture) | Menu |
| GET/POST | `/api/tables` | Gérant / lecture | Tables et leur état |
| POST | `/api/commandes` | Serveur | Créer une commande (brouillon) |
| POST | `/api/commandes/:id/envoyer` | Serveur | Envoyer en cuisine |
| PATCH | `/api/commandes/:id/lignes/:lid/statut` | Cuisinier/Serveur | Changer le statut d'une ligne |
| POST | `/api/commandes/:id/payer` | Caissier | Encaisser, créer la facture |
| GET | `/api/factures`, `/api/factures/:id/pdf` | Caissier/Gérant | Factures |
| GET | `/api/dashboard/*` | Gérant | Ventes, top plats |
| GET/POST | `/api/utilisateurs` | Gérant | Comptes |
| WS | `/ws` | tous | Événements temps réel (nouvelle commande, changement de statut) |

## 6. Sécurité

- Mots de passe hachés (bcrypt/argon2), jamais stockés en clair.
- Sessions/JWT avec expiration ; déconnexion automatique après inactivité.
- Rôles vérifiés côté serveur sur **chaque** route (pas seulement côté interface).
- Sauvegarde quotidienne automatique de la base + test de restauration mensuel.
- Application servie en HTTPS si exposée hors du réseau local.

---

*Proposition soumise à revue d'architecture. Les décisions figées seront notées « ADR » (Architecture Decision Records) dans `docs/adr/`.*
