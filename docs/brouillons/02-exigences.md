# 02 — Analyse des exigences

**Projet :** Chez Mama Rita
**Date :** 2026-11-04
**Statut :** Brouillon à valider

Priorisation **MoSCoW** : M = Must (indispensable V1), S = Should (souhaitable V1), C = Could (si le temps le permet), W = Won't (hors périmètre V1).

---

## 1. Exigences fonctionnelles (EF)

### 1.1 Gestion du menu (rôle : Gérant)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-01 | Créer un plat (nom, description, prix en XOF, catégorie, photo optionnelle) | M | Le plat apparaît immédiatement dans la carte des serveurs |
| EF-02 | Modifier le prix ou la description d'un plat | M | Le nouveau prix s'applique aux nouvelles commandes |
| EF-03 | Supprimer / archiver un plat | S | Un plat archivé n'est plus commandable mais reste dans l'historique |
| EF-04 | Marquer un plat comme disponible / indisponible (rupture) | M | Un plat indisponible est grisé et non sélectionnable par le serveur |
| EF-05 | Organiser les plats par catégories (entrées, plats, boissons, desserts…) | M | Filtres par catégorie dans la prise de commande |

### 1.2 Gestion des tables (rôle : Gérant)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-06 | Créer / modifier / supprimer des tables (numéro, capacité, zone : salle, terrasse…) | M | La salle est représentée fidèlement |
| EF-07 | Visualiser l'état de chaque table (libre, occupée, commande en cours, à encaisser) | M | Vue d'ensemble de la salle en un écran |

### 1.3 Prise de commandes (rôle : Serveur)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-08 | Ouvrir une commande sur une table et y associer le serveur connecté | M | La commande est horodatée et rattachée au bon serveur |
| EF-09 | Ajouter des plats à la commande avec quantités et commentaire (ex : « sans piment ») | M | Chaque ligne affiche plat, quantité, prix unitaire, total |
| EF-10 | Modifier / supprimer une ligne avant envoi en cuisine | M | — |
| EF-11 | Envoyer la commande à la cuisine (validation) | M | La commande apparaît instantanément sur l'écran cuisine |
| EF-12 | Ajouter des plats à une commande déjà envoyée (commande complémentaire) | S | La cuisine reçoit une notification de la nouvelle ligne |

### 1.4 Transmission et suivi cuisine (rôles : Serveur, Cuisinier)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-13 | Affichage automatique des commandes sur l'écran cuisine, triées par ancienneté | M | Sans aucune action du cuisinier |
| EF-14 | Statuts d'une commande : *En attente → En préparation → Prêt → Servi → Payée* | M | Chaque changement est horodaté et visible de la salle |
| EF-15 | Le cuisinier marque une ligne / une commande « en préparation » puis « prêt » | M | Le serveur voit le changement en temps réel |
| EF-16 | Le serveur marque la commande « servie » | S | — |
| EF-17 | Annuler une commande (avec motif) si elle n'est pas encore en préparation | S | Trace conservée pour le gérant |

### 1.5 Paiements et factures (rôle : Caissier)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-18 | Générer la facture d'une table : liste des plats, quantités, prix, total TTC | M | Calcul automatique, zéro erreur d'arrondi (montants entiers XOF) |
| EF-19 | Encaisser en espèces avec saisie du montant reçu et calcul automatique du rendu | M | Le rendu est calculé et affiché |
| EF-20 | Facture imprimable / affichable (PDF ou ticket) avec numéro de facture, date, heure | M | Un numéro unique par facture |
| EF-21 | Réimpression / consultation des factures passées | S | Recherche par date, table ou numéro |
| EF-22 | Clôturer la table après paiement (elle redevient libre) | M | — |

### 1.6 Tableau de bord (rôle : Gérant)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-23 | Chiffre d'affaires du jour / période (par jour, semaine, mois) | M | Filtre de période |
| EF-24 | Nombre de commandes et de couverts | M | — |
| EF-25 | Top des plats les plus commandés (quantités et montant) | M | Classement sur la période choisie |
| EF-26 | Ventes par catégorie et par serveur | S | — |

### 1.7 Comptes et sécurité (rôle : Gérant)

| ID | Exigence | Priorité | Critère d'acceptation |
|----|----------|----------|----------------------|
| EF-27 | Connexion par identifiant + mot de passe, avec rôle (Serveur, Cuisinier, Caissier, Gérant) | M | Chaque rôle n'accède qu'à ses fonctions |
| EF-28 | Le gérant crée / désactive des comptes utilisateurs | M | Un compte désactivé ne peut plus se connecter |
| EF-29 | Journal des actions sensibles (annulations, changements de prix, encaissements) | S | Consultation par le gérant avec date et utilisateur |

## 2. Exigences non fonctionnelles (ENF)

| ID | Exigence | Priorité | Détail |
|----|----------|----------|--------|
| ENF-01 | Disponibilité | M | L'application fonctionne sur le réseau local du restaurant, même si Internet est coupé (données servies localement) |
| ENF-02 | Temps de réponse | M | Affichage d'une commande en cuisine < 3 s après envoi (temps réel via WebSocket/SSE) |
| ENF-03 | Simplicité d'usage | M | Prise en main < 15 min pour un serveur ; écrans épurés, grands boutons (tablette) |
| ENF-04 | Responsive | M | Utilisable sur tablette (serveurs), écran cuisine, poste caisse |
| ENF-05 | Sécurité | M | Mots de passe hachés, sessions sécurisées, HTTPS si exposé, sauvegardes automatiques quotidiennes de la base |
| ENF-06 | Sauvegarde | M | Sauvegarde locale automatique + export manuel ; restauration testée |
| ENF-07 | Données | M | Toutes les commandes et factures conservées (historique illimité, archivage manuel possible) |
| ENF-08 | Multi-utilisateur simultané | M | Plusieurs serveurs peuvent prendre des commandes en parallèle sans conflit |
| ENF-09 | Impression | S | Impression des tickets/factures sur imprimante locale (ou génération PDF si pas d'imprimante) |
| ENF-10 | Langue / devise | M | Français, montants en XOF (entiers) |

## 3. Matrice acteurs × fonctionnalités

| Fonctionnalité | Serveur | Cuisinier | Caissier | Gérant |
|----------------|:-------:|:---------:|:--------:|:------:|
| Menu (plats/prix/dispo) | lecture | lecture | lecture | **CRUD** |
| Tables | lecture | — | lecture | **CRUD** |
| Prise de commande | **création** | — | lecture | lecture |
| Transmission cuisine / statuts | lecture | **mise à jour** | — | lecture |
| Factures / paiements | — | — | **création** | lecture |
| Tableau de bord | — | — | lecture | **consultation** |
| Comptes utilisateurs | — | — | — | **CRUD** |

---

*À valider avant de figer l'architecture et le plan de travail.*
