# Étude de santé publique — sous-nutrition mondiale

**Compétences mobilisées :** Python · pandas · numpy · matplotlib

---

## Contexte & besoin métier

Déterminer si la production alimentaire mondiale suffirait à nourrir la population mondiale, et identifier les pays où cibler en priorité l'aide alimentaire.

## Données

4 fichiers FAO (population, disponibilité alimentaire, aide alimentaire, sous-nutrition), avec des unités hétérogènes (milliers de tonnes, milliers de personnes) à harmoniser avant toute comparaison.

## Démarche

Harmonisation systématique des unités en amont (population et sous-nutrition ramenées en nombre de personnes, disponibilité alimentaire en kg) — sans cette étape, toute comparaison entre tables est faussée. Calcul du nombre théorique de personnes que la disponibilité alimentaire mondiale pourrait nourrir, décomposé ensuite en produits végétaux seuls versus produits animaux seuls, pour objectiver le rendement calorique très supérieur d'un régime végétal. Identification des 10 pays au taux de sous-nutrition le plus élevé et des 5 pays ayant le plus bénéficié d'aide alimentaire depuis 2013. Deux études de cas ciblées pour illustrer des dynamiques différentes : Haïti (évolution croisée population / sous-nutrition / aide dans le temps) et la Thaïlande (taux d'exportation du manioc rapporté à la disponibilité intérieure).

## Résultats

La disponibilité alimentaire mondiale suffit largement à nourrir la population mondiale — et suffirait encore davantage si elle était orientée vers les produits végétaux plutôt qu'animaux. La sous-nutrition est donc avant tout un problème de répartition, pas de production. Liste des pays prioritaires pour l'aide alimentaire établie, avec des tendances par pays parfois contre-intuitives : la Thaïlande exporte une part significative de sa production de manioc, l'ouverture commerciale d'un pays n'étant pas nécessairement corrélée à un déficit alimentaire local.

## Limites & pistes

L'agrégation mondiale masque les difficultés réelles de distribution (transport, conflits, stockage) qui expliquent en partie l'écart entre disponibilité théorique et accès réel à la nourriture. L'analyse de la sous-nutrition reste centrée sur une seule année (2017).

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
