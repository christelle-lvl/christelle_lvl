# Analyse sociodémographique avec dbt — architecture de données et restitution Power BI

**Compétences mobilisées :** dbt (staging/intermediate/mart, tests) · Snowflake · Power BI

---

## Contexte & besoin métier

Fiabiliser et industrialiser le traitement de données sociodémographiques (effectifs, genre, âge, région) pour produire des indicateurs de proportion d'étudiants par population, en remplaçant des traitements ad hoc par un pipeline de transformation testé et documenté.

## Données

Données démographiques et de population par année (tables `DEMOGRAPHIC` et `POP2022` à `POP2025`), hébergées sur Snowflake dans une base `DATA_DEMO_DBT` / schéma `RAW`, avec une vigilance RGPD sur le caractère anonymisé des données individuelles.

## Démarche

Mise en place d'une architecture dbt en couches plutôt qu'un enchaînement de requêtes SQL non versionnées : une couche *staging* pour nettoyer et typer chaque source indépendamment (`stg_demographic`, `stg_pop2022` à `stg_pop2025`), une couche *intermediate* pour les premières agrégations et harmonisations (`int_demographic`, `int_insee_pop`), et une couche *mart* exposant l'indicateur final (`mart_proportion_students_pop`). Une table de correspondance (bridge table) est construite spécifiquement pour harmoniser les tranches d'âge entre les différentes sources, qui ne découpent pas la population selon les mêmes bornes. Des tests de qualité sont intégrés directement dans la configuration dbt plutôt que vérifiés manuellement : tests `not_null` sur les champs identifiants et structurants (ID étudiant, genre, région, filière) et test `accepted_values` sur la variable de tranche d'âge pour garantir qu'aucune valeur hors nomenclature ne se propage dans les couches suivantes. L'ensemble des dépendances entre modèles est documenté via le DAG généré par dbt, qui rend explicite le chemin de transformation de la donnée brute jusqu'à l'indicateur final. Les données sont ensuite restituées dans Power BI.

## Résultats

Un pipeline de transformation traçable et testé, avec un DAG documentant précisément comment chaque table brute contribue à l'indicateur final. Restitution Power BI présentant la répartition des étudiants par genre, la distribution par tranche d'âge, une cartographie territoriale des effectifs, l'évolution temporelle 2022-2025, et le nombre d'étudiants rapporté à la population (pour 100 000 habitants) par région — un indicateur qui neutralise les effets de taille de population entre régions et permet une comparaison équitable.

## Limites & pistes

La table de correspondance des tranches d'âge est un choix de modélisation qui mériterait d'être revalidé si de nouvelles sources aux découpages différents venaient s'ajouter. Les tests actuels couvrent la structure (valeurs nulles, valeurs acceptées) mais pas encore la cohérence métier inter-tables (par exemple un contrôle de cohérence des totaux entre couches), qui serait une évolution naturelle du dispositif de tests.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
