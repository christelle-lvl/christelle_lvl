# Diagnostic stock, ventes et marge — site e-commerce Bottleneck

**Compétences mobilisées :** Python · pandas · numpy · plotly · détection d'outliers (z-score, IQR) · analyse Pareto · analyse de corrélation

---

## Contexte & besoin métier

Produire un diagnostic fiable de l'activité d'un site e-commerce (chiffre d'affaires, produits performants, état des stocks, rentabilité) à partir de trois sources internes jamais consolidées.

## Données

3 fichiers (ERP : prix et stock, site web : ventes, table de correspondance entre les deux systèmes) — incohérences multiples à la source : prix et stocks négatifs, deux colonnes de statut de stock parfois contradictoires entre elles, codes articles mal formatés, doublons, lignes sans correspondance entre systèmes.

## Démarche

Nettoyage méthodique avant toute jointure, plutôt qu'un nettoyage a posteriori sur des données déjà fusionnées. Vérification systématique de la cohérence entre colonnes redondantes (le statut de stock recalculé est comparé à la colonne existante avant correction). Correction des valeurs négatives : les prix sont repassés en positif après avoir vérifié leur cohérence avec la marge habituellement appliquée (x2), les stocks négatifs sont ramenés à 0 — un choix assumé et documenté plutôt qu'une correction silencieuse. Suppression des doublons et des lignes sans code article valide, la validité étant vérifiée par expression régulière plutôt que par inspection manuelle. Jointures successives des 3 tables en contrôlant à chaque étape le nombre de lignes sans correspondance. Détection des prix aberrants par deux méthodes complémentaires (z-score et intervalle interquartile), pour ne pas dépendre d'une seule règle de décision. Analyse du chiffre d'affaires et des volumes selon le principe 20/80, calcul de la rotation de stock et de la valorisation financière du stock immobilisé, analyse du taux de marge par famille de produit et des corrélations entre stock, prix et ventes.

## Résultats

Chiffre d'affaires total calculé avec et sans les valeurs aberrantes, confirmation que la loi de Pareto s'applique à ce catalogue (une petite part des articles génère l'essentiel du chiffre d'affaires et des ventes en volume), identification des articles à rotation de stock excessive représentant du capital immobilisé inutilement, taux de marge par catégorie de produit permettant de prioriser les familles à pousser commercialement. Corrélation modérée positive entre stock et ventes, modérée négative entre prix et ventes. Un fichier consolidé et nettoyé livré en Excel, directement exploitable par les équipes métier sans repasser par le code.

## Limites & pistes

Les règles de nettoyage (stocks négatifs ramenés à 0, par exemple) sont des choix assumés faute de pouvoir remonter à la cause réelle des anomalies dans les systèmes sources — à valider avec les équipes IT/ERP avant une industrialisation. L'étude reste un instantané et ne permet pas de suivre l'évolution du stock ou de la marge dans le temps.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
