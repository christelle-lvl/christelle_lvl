# Étude de marché à l'export — poulet biologique

**Compétences mobilisées :** Python · pandas · scikit-learn · scipy · plotly · seaborn · nettoyage multi-source · ACP · CAH · K-means

**En une phrase :** Une segmentation de 131 pays en 4 profils de marché, croisant richesse, logistique et habitudes de consommation, pour prioriser les marchés d'export du poulet biologique.

---

## Contexte & besoin métier

Identifier les marchés d'export prioritaires pour du poulet biologique. Avant toute collecte de données, cadrage du besoin via une grille PESTEL (politique, économique, social, technologique, environnemental) : chaque axe est traduit en une variable mesurable et justifiée (ex. stabilité politique = risque contractuel et douanier, indice logistique = capacité à recevoir des produits réfrigérés). Cette structuration en amont évite de collecter des données au hasard puis de chercher a posteriori ce qu'on peut en faire.

## Données

- 5 sources hétérogènes (FAO et Banque mondiale) : disponibilité alimentaire, population, indice de performance logistique (LPI), PIB par habitant, stabilité politique, part de l'agriculture dans le PIB
- Formats disparates : encodages différents (UTF-8 / latin-1), séparateurs différents, virgules décimales à convertir
- Données croisées sur l'année 2017 (année commune la plus complète entre les sources)

## Démarche

**1. Harmonisation multi-source** — Les 5 tables nomment parfois un même pays différemment (« République-Unie de Tanzanie » vs « Tanzanie »), incluent des agrégats régionaux de la Banque mondiale (« Afrique subsaharienne ») et des territoires non-souverains (Guadeloupe, Porto Rico) qu'il faut exclure du périmètre pays. Un dictionnaire de correspondance et des listes d'exclusion documentées permettent une jointure propre des 5 tables.

**2. Traitement différencié des valeurs manquantes** — Exclusion stricte des pays sans donnée sur les variables de marché (import/export/consommation — 36 pays exclus, aucune imputation possible sur une mesure commerciale absente) ; imputation par la médiane pour les variables contextuelles facultatives (LPI, PIB, stabilité, agriculture). Choix assumé et documenté sur la Chine : sa stabilité politique n'est pas renseignée pour 2017, mais elle reste écartée à tort si on l'exclut sur ce seul critère — la valeur est imputée plutôt que le pays supprimé.

**3. Contrôle de représentativité avant analyse** — Vérification explicite que l'échantillon final (131 pays) couvre un objectif de représentativité fixé au départ : 88,8 % de la population mondiale, au-delà du seuil de 60 % visé.

**4. Exploration avant modélisation** — Distributions, boxplots et matrice de corrélation systématiques. Les outliers identifiés (Chine et Inde sur la population, Luxembourg sur le PIB/habitant) ne sont pas supprimés : ce sont des pays réels aux profils extrêmes, pas des erreurs. 5 variables à distribution très asymétrique sont transformées en logarithme pour éviter que 2-3 pays dominent à eux seuls les axes de l'ACP.

**5. ACP (réduction de dimension)** — Réduction à 3 axes retenus (79,7 % de variance expliquée), en arbitrant entre la règle de Kaiser (qui n'en retiendrait que 2) et le seuil conventionnel de 80 % — le 3ᵉ axe est conservé car son apport reste substantiel pour la finesse des groupes obtenus, pour une perte d'information marginale. PC1 (48 %) résume le niveau de développement économique du pays, PC2 (22 %) sa taille et son volume commercial.

**6. Double clustering pour robustesse** — Une classification ascendante hiérarchique (CAH, méthode de Ward) d'abord, un k-means ensuite pour confirmer la structure trouvée par une méthode indépendante. Les deux convergent vers 4 groupes cohérents. Le choix de k=4 plutôt que k=2 (optimum mathématique au score de silhouette) est un compromis assumé : 2 groupes seraient trop grossiers pour l'usage métier et masqueraient un marché de niche à forte consommation par habitant.

## Résultats

**4 profils de marché identifiés** parmi 131 pays :

| Cluster | Pays | Profil |
|---|---|---|
| **4 — Cible prioritaire** | 26 (Chine, Allemagne, États-Unis, Japon...) | PIB et logistique les plus élevés, forte consommation, agriculture la plus faible |
| **2 — Marché de niche** | 31 (petits États stables) | Consommation par habitant la plus élevée du jeu de données (31,9 kg/hab) |
| **3 — À surveiller** | 25 (grands pays émergents) | Volumes commerciaux élevés mais stabilité politique la plus faible |
| **1 — Non prioritaire** | 49 | PIB et consommation les plus faibles, agriculture dominante |

Le livrable va au-delà de la segmentation : deux plans d'action concrets, construits à partir du solde commercial (imports moins exports) du cluster prioritaire. **Plan A (marché mondial)** : Japon, Royaume-Uni, Émirats arabes unis, Allemagne, Corée du Sud en tête. **Plan B (marché européen)** : Royaume-Uni, Allemagne, Tchéquie, Suède, Suisse.

## Limites & pistes

- L'échantillon exclut 36 pays faute de données commerciales exploitables (dont Madagascar, Tanzanie) — des marchés non analysables avec ces sources, pas nécessairement sans potentiel.
- Le choix de 4 clusters est un compromis métier plutôt qu'un optimum statistique strict (le score de silhouette pointait vers 2 groupes) — défendable, mais assumé clairement plutôt que présenté comme une évidence mathématique.
- L'étude reste au niveau macro (indicateurs pays) : elle n'intègre pas la réglementation spécifique au bio ni les barrières douanières précises par marché.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
