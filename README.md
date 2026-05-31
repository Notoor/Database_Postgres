# Système de Gestion Commerciale - PostgreSQL

## Description

Ce projet implémente une base de données PostgreSQL destinée à la gestion commerciale d'une entreprise. Elle permet de gérer les clients, les fournisseurs, les employés, les produits ainsi que les ventes réalisées.

L'objectif est de centraliser les informations et de faciliter le suivi des activités commerciales.

---

## Structure de la Base de Données

### Tables principales

#### Clients

Contient les informations relatives aux clients.

| Champ     | Type    | Description                  |
| --------- | ------- | ---------------------------- |
| ClientID  | SERIAL  | Identifiant unique du client |
| Nom       | VARCHAR | Nom du client                |
| Prenom    | VARCHAR | Prénom du client             |
| Adresse   | TEXT    | Adresse du client            |
| Email     | VARCHAR | Adresse e-mail               |
| NumeroTel | VARCHAR | Numéro de téléphone          |

#### Fournisseurs

Contient les informations des fournisseurs.

| Champ           | Type    | Description         |
| --------------- | ------- | ------------------- |
| FournisseurID   | SERIAL  | Identifiant unique  |
| NomFournisseur  | VARCHAR | Nom du fournisseur  |
| Adresse         | TEXT    | Adresse             |
| Email           | VARCHAR | Adresse e-mail      |
| NumeroTelephone | VARCHAR | Numéro de téléphone |

#### Employes

Contient les informations des employés.

| Champ     | Type    | Description         |
| --------- | ------- | ------------------- |
| EmployeID | SERIAL  | Identifiant unique  |
| Nom       | VARCHAR | Nom                 |
| Prenom    | VARCHAR | Prénom              |
| Fonction  | VARCHAR | Poste occupé        |
| Email     | VARCHAR | Adresse e-mail      |
| NumeroTel | VARCHAR | Numéro de téléphone |

#### Produits

Contient les produits commercialisés.

| Champ         | Type    | Description              |
| ------------- | ------- | ------------------------ |
| ProduitID     | SERIAL  | Identifiant unique       |
| NomProduit    | VARCHAR | Nom du produit           |
| Description   | TEXT    | Description du produit   |
| PrixUnitaire  | NUMERIC | Prix unitaire            |
| FournisseurID | INT     | Référence du fournisseur |

#### Ventes

Enregistre les transactions effectuées.

| Champ     | Type    | Description            |
| --------- | ------- | ---------------------- |
| VenteID   | SERIAL  | Identifiant unique     |
| DateVente | DATE    | Date de la vente       |
| Quantite  | INT     | Quantité vendue        |
| Montant   | NUMERIC | Montant total          |
| ClientID  | INT     | Référence du client    |
| ProduitID | INT     | Référence du produit   |
| EmployeID | INT     | Référence de l'employé |

---

## Relations

* Un fournisseur peut fournir plusieurs produits.
* Un produit appartient à un seul fournisseur.
* Un client peut effectuer plusieurs achats.
* Un employé peut enregistrer plusieurs ventes.
* Une vente concerne un seul produit, un seul client et un seul employé.

---

## Installation

### Prérequis

* PostgreSQL 14 ou supérieur
* pgAdmin (optionnel)

### Création de la base de données

```sql
CREATE DATABASE gestion_commerciale;
```

### Connexion à la base

```bash
psql -U postgres -d gestion_commerciale
```

### Exécution du script

```bash
psql -U postgres -d gestion_commerciale -f schema.sql
```

---

## Fonctionnalités

* Gestion des clients
* Gestion des fournisseurs
* Gestion des employés
* Gestion des produits
* Enregistrement des ventes
* Analyse du chiffre d'affaires
* Suivi des performances commerciales

---

## Exemple de requête

Afficher toutes les ventes :

```sql
SELECT
    v.VenteID,
    v.DateVente,
    c.Nom AS Client,
    p.NomProduit,
    e.Nom AS Employe,
    v.Quantite,
    v.Montant
FROM Ventes v
JOIN Clients c ON v.ClientID = c.ClientID
JOIN Produits p ON v.ProduitID = p.ProduitID
JOIN Employes e ON v.EmployeID = e.EmployeID;
```

---

## Auteur

Projet de base de données PostgreSQL réalisé dans le cadre d'un système de gestion commerciale.

## Licence

Usage académique et pédagogique.
