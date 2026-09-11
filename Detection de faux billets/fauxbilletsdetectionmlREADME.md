# Détection automatique de faux billets

**Compétences mobilisées :** Python · pandas · scikit-learn · seaborn · régression logistique · random forest · KNN · validation croisée

**En une phrase :** Un modèle de classification qui identifie les faux billets à partir de 6 mesures géométriques, avec un rappel de 98 % sur la classe la plus coûteuse à manquer.

---

## Contexte & besoin métier

L'ONCFM (Organisation nationale de lutte contre le faux-monnayage) souhaite pouvoir identifier automatiquement les faux billets à partir de leurs seules caractéristiques géométriques (dimensions, marges), sans expertise humaine poussée. L'enjeu métier est asymétrique : un faux billet classé à tort comme authentique (faux négatif) coûte bien plus cher qu'un vrai billet signalé par erreur (faux positif). Le critère de succès n'est donc pas l'exactitude globale du modèle, mais sa capacité à détecter les faux.

## Données

- 1 500 billets, 6 mesures géométriques (diagonale, hauteurs gauche/droite, marges basse/haute, longueur) + un label vrai/faux
- Aucun doublon
- 37 valeurs manquantes (2,5 %) sur une seule variable, `margin_low`

## Démarche

**1. Exploration** — Les distributions de plusieurs variables selon vrai/faux montrent déjà une séparation nette entre les deux classes, avant tout modèle.

**2. Traitement des valeurs manquantes** — Plutôt que de supprimer les lignes incomplètes ou d'imputer par la médiane, test d'une régression linéaire (basée sur la forte corrélation de `margin_low` avec les autres mesures, notamment -0,67 avec la longueur) comparée par validation croisée à 5 plis : la régression réduit l'erreur moyenne d'un tiers par rapport à la médiane (MAE 0,38 mm contre 0,57 mm). C'est ce résultat mesuré, et non une préférence a priori, qui a tranché le choix de la méthode d'imputation.

**3. Préparation** — Séparation train/test stratifiée (80/20) pour vérifier que le modèle généralise à des billets jamais vus, et standardisation des variables (nécessaire pour la régression logistique, le KNN et le k-means, sensibles à l'échelle ; inutile pour le random forest).

**4. Comparaison de 4 modèles** — régression logistique, k-means détourné en classification (2 clusters rattachés à la classe majoritaire), KNN (k=5), random forest. Choisir plusieurs méthodes plutôt qu'une seule permet de vérifier que le signal est robuste et pas un artefact d'un algorithme en particulier.

**5. Critère de sélection** — Le modèle final n'est pas choisi sur l'accuracy globale mais sur le rappel de la classe "faux", conformément à l'asymétrie du coût d'erreur pour l'ONCFM.

## Résultats

| Modèle | Rappel faux | Précision faux | Accuracy |
|---|---|---|---|
| **Régression logistique** | **0,98** | 0,99 | 0,99 |
| Random Forest | 0,98 | 0,99 | 0,99 |
| K-means | 0,98 | 0,98 | 0,987 |
| KNN | 0,97 | 0,98 | 0,983 |

Régression logistique et random forest arrivent à égalité stricte sur toutes les métriques. La régression logistique est retenue comme modèle final : à résultat identique, c'est le plus simple et le plus interprétable des deux, ce qui facilite l'explication des décisions du modèle à l'ONCFM. Sur 100 faux billets soumis, 98 sont correctement détectés. Le modèle est sérialisé et prêt à être réutilisé sur de nouveaux billets.

## Limites & pistes

- Rappel de 0,98 signifie que 2 % des faux billets passent encore au travers — un risque résiduel à documenter auprès de l'ONCFM, pas à masquer.
- Le seuil de décision de la régression logistique est resté à sa valeur par défaut (0,5) : une analyse de la courbe précision-rappel permettrait probablement de gagner encore un peu de rappel, au prix d'un peu de précision.
- Le modèle est entraîné sur 1 500 billets d'une seule série ; sa capacité à généraliser à des contrefaçons plus récentes ou plus sophistiquées n'est pas garantie et mériterait d'être revalidée périodiquement.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
