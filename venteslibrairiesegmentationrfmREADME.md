# Analyse des ventes d'une librairie — diagnostic, tests statistiques et segmentation client

**Compétences mobilisées :** Python · pandas · numpy · matplotlib/seaborn · scikit-learn (StandardScaler, K-Means, PCA) · scipy.stats (Shapiro, Chi², V de Cramér)

---

## Contexte & besoin métier

Produire un diagnostic complet des ventes d'une librairie (mars 2021 - février 2023) — évolution du chiffre d'affaires, comportement client, qualité des données — puis aller plus loin en segmentant la clientèle pour des actions marketing ciblées.

## Données

Historique de ventes, catalogue produits et base clients sur deux ans, avec une anomalie de qualité de données significative détectée en amont : un bloc de 361 041 lignes vides dans les transactions, à traiter avant toute analyse pour ne pas fausser les agrégats.

## Démarche

Ce projet a la particularité d'avoir été repris et optimisé à l'aide de l'IA à partir d'une version pédagogique originale, avec une **traçabilité complète assumée comme démarche** : chaque cellule d'origine est conservée dans un bloc archivé, accompagnée d'un tableau de justification du choix méthodologique, avant la version optimisée — une manière de documenter non seulement le résultat mais la démarche d'amélioration elle-même.

Le nettoyage sécurise les jointures avec `validate="many_to_one"` pour détecter toute anomalie de cardinalité invisible à l'œil nu, corrige des noms de mois codés en dur en français (source de bugs sur les tris chronologiques), et remplace un comptage figé du catalogue par un calcul dynamique. L'analyse temporelle utilise une moyenne mobile sur 7 jours plutôt que la série brute pour lisser le bruit quotidien et fait apparaître une baisse de chiffre d'affaires d'environ 4 000 € en novembre 2021, investiguée spécifiquement plutôt que laissée inexpliquée. Une courbe de Lorenz objective la concentration de la clientèle (5 % des clients génèrent 80 % du chiffre d'affaires) et sert de base à la détection des comptes B2B : un examen de la distribution du nombre de sessions fait apparaître une rupture nette au-delà de 2 000 sessions, qui permet d'isoler 4 clients B2B et de les exclure des analyses B2C pour ne pas biaiser les profils clients. La robustesse statistique est vérifiée systématiquement (test de Shapiro pour la normalité, skewness/kurtosis, test du Chi² et V de Cramér pour l'association genre × catégorie de produit) avec une vigilance explicite sur le biais de significativité lié aux grands échantillons.

Une **étape de segmentation client (RFM + K-Means)** vient enrichir l'analyse initiale : construction des variables Récence/Fréquence/Montant (hors clients B2B), standardisation, choix du nombre de clusters croisant méthode du coude et score de silhouette plutôt qu'un seul critère, profilage des segments obtenus, visualisation par réduction de dimension (PCA à 2 composantes), puis étiquetage métier automatisé des segments via des règles de décision (`np.select`) — un étiquetage explicitement présenté comme indicatif, à valider avec les équipes marketing avant exploitation opérationnelle.

## Résultats

Un diagnostic fiabilisé des ventes avec une anomalie de données majeure détectée et traitée en amont plutôt que propagée dans les analyses. La baisse de novembre 2021 identifiée et documentée. Une segmentation B2B/B2C objectivée par la donnée plutôt que par une liste métier a priori. Des segments clients RFM profilés et visualisés, avec des libellés métier proposés comme point de départ pour une action marketing ciblée.

## Limites & pistes

Les libellés métier attribués aux segments RFM sont générés par une règle de décision et restent à valider par les équipes marketing avant toute campagne. Le test du Chi² sur un grand échantillon peut signaler une association statistiquement significative mais d'ampleur négligeable en pratique (V de Cramér à interpréter conjointement). La démarche d'optimisation assistée par IA, bien que tracée intégralement, reste construite sur un notebook pédagogique original et non sur un cas de production réel.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
