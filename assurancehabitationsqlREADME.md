# Base de données assurance habitation — modélisation et requêtage SQL

**Compétences mobilisées :** MySQL · modélisation UML · Excel (étude préalable)

---

## Contexte & besoin métier

Structurer une base de données d'assurance habitation à partir de fichiers plats (contrats, référentiel géographique) pour permettre des analyses fiables — impossibles à mener correctement dans un tableur au-delà de quelques milliers de lignes.

## Données

2 fichiers sources (contrats, région), reliés par une clé commune reconstruite par concaténation (`Code_dep_code_commune`).

## Démarche

Étude préalable dans Excel pour repérer les liens et clés candidates avant toute création de table. Modélisation UML du schéma relationnel (choix des clés primaires/étrangères, typage précis des colonnes) plutôt qu'un import brut des fichiers. Création des tables et import dans MySQL (38 916 + 30 335 lignes). Requêtes construites en LEFT JOIN systématique pour ne perdre aucun contrat orphelin de région, avec agrégations (GROUP BY, HAVING) pour répondre à des questions métier concrètes.

## Résultats

Base interrogeable permettant de répondre à des questions métier directes : cotisation mensuelle moyenne par département, communes avec le plus grand nombre de contrats, répartition des contrats par tranche de valeur déclarée des biens, surface moyenne assurée par région.

## Limites & pistes

Le modèle reste sur 2 tables ; une base assurance en production intégrerait aussi sinistres et clients. Aucun contrôle d'intégrité automatisé au-delà de la contrainte de clé étrangère posée manuellement.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
