# Priorisation de l'aide au développement des infrastructures d'eau potable

**Compétences mobilisées :** Power BI · Power Query · DAX · modélisation de données · aide à la décision

**En une phrase :** Un dashboard Power BI qui croise accès à l'eau, assainissement et stabilité politique pour identifier les pays où un déploiement d'infrastructures serait le plus pertinent.

---

## Contexte & besoin métier

DWFA souhaite décider où investir en priorité dans le développement d'infrastructures d'accès à l'eau potable. La décision ne peut pas se limiter au seul taux d'accès à l'eau : un pays très en retard mais politiquement instable ne peut pas absorber un projet d'infrastructure lourd. Le dashboard sert d'outil d'aide à la décision pour arbitrer entre trois types d'intervention selon le niveau de développement déjà atteint par chaque pays, plutôt que de produire un classement à plat.

## Données

- Indicateurs par pays et par année (2000-2020) : accès à l'eau potable (%), accès à l'eau assainie (%), stabilité politique (indice), mortalité, population urbaine/rurale, région OMS
- **Source :** Organisation mondiale de la santé (OMS)
- **Nettoyage / transformations :** préparation et jointures de plusieurs tables sources réalisées dans Power Query, pour obtenir un modèle unique croisant pays, année et indicateurs

## Démarche

**1. Modélisation navigable** — Construction d'un modèle de données permettant un filtrage dynamique à plusieurs niveaux (année, région, pays, plage d'accès à l'eau, plage de stabilité politique), avec 4 pages de lecture : national, régional, mondial, pays candidats.

**2. Croisement systématique** — Plutôt que de classer les pays sur le seul critère de l'accès à l'eau, croisement de cet indicateur avec la stabilité politique (nuages de points "Efficacité politique vs stabilité politique", "Impact de la stabilité politique sur l'accès à l'eau"). Un pays avec un fort besoin mais politiquement instable n'est pas un bon candidat à un investissement lourd.

**3. Segmentation en 3 domaines d'intervention** — Définition de seuils différenciés d'accès à l'eau, à l'assainissement et de stabilité politique pour 3 types d'action : création de services (rien n'existe), modernisation (une base existe déjà), consulting (le pays est déjà avancé). Cette segmentation traduit le besoin métier en critère actionnable, plutôt qu'un classement brut peu exploitable pour décider.

**4. Filtrage final** — Application des seuils du segment prioritaire (accès eau potable 30-70 %, accès eau assainie 10-50 %, stabilité politique > -1) pour isoler une liste resserrée de pays candidats.

## Résultats

**9 pays identifiés comme candidats prioritaires** pour une création d'infrastructures : Bénin, Guinée, Madagascar, Malawi, Mozambique, Ouganda, Tanzanie, Togo, Zimbabwe — des pays où l'accès à l'eau reste faible tout en conservant une stabilité politique suffisante pour envisager un projet d'infrastructure.

Le dashboard reste interactif : le commanditaire peut lui-même ajuster les curseurs de seuil selon ses contraintes du moment, sans redemander une nouvelle analyse à chaque changement de critère.

## Limites & pistes

- Les seuils des 3 domaines d'intervention sont définis a priori. Ils mériteraient d'être challengés avec le commanditaire, ou recalés sur des données de coût réel de projets comparables plutôt que sur des paliers arbitraires.
- L'indice de stabilité politique est un indicateur composite dont la méthodologie de calcul n'est pas questionnée ici — un pays peut être mal noté pour des raisons qui n'empêchent pas concrètement un projet ciblé localement.
- L'analyse n'intègre pas de dimension de coût ni de faisabilité logistique (accès géographique, présence d'acteurs locaux sur le terrain), qui serait l'étape suivante avant une décision d'investissement.

---

*Projet réalisé dans le cadre de la formation Data Analyst — OpenClassrooms.*
*Portfolio complet : [lien à venir]*
