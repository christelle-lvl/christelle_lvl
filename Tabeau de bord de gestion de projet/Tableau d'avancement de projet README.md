# Dashboard de suivi d'avancement de projet — Power BI

**Contexte & besoin métier :** Donner à des équipes projet un outil de pilotage unique et dynamique permettant de suivre en temps réel l'avancement d'un projet (budget, délais, livrables) plutôt que de s'appuyer sur des reportings ponctuels et dispersés.

**Données :** Données de suivi de projet (phases, livrables, budget prévisionnel/réel, planning) structurées pour alimenter un modèle Power BI multi-pages.

**Démarche :** Construction d'un rapport de 9 pages organisées par niveau de lecture plutôt qu'un tableau unique surchargé : une page d'accueil/navigation, une page "Général" avec des jauges de suivi (budget, livrables, durée), une carte Azure Maps pour la dimension géographique du projet et un graphique d'alertes, une page "Performance financière et livrables" dédiée au suivi budgétaire, une page "Délai et planning" avec un diagramme de Gantt pour visualiser l'enchaînement des tâches, une page "Détail des phases" avec des nuages de points pour comparer les phases entre elles, une page de questions-réponses en langage naturel (Q&A) pour permettre une exploration libre des données sans dépendre des pages pré-construites, une page d'analyse graphique complémentaire, et une page "Modèle de données" documentant la structure sous-jacente. Un indicateur central — l'indice d'écart — mesure en continu le décalage entre le prévisionnel et le réalisé (budget, durée, livrables), calculé en DAX et repris sur plusieurs pages du rapport pour donner un signal d'alerte cohérent.

**Résultats :** Un dashboard interactif unique remplaçant plusieurs reportings statiques, permettant à une équipe projet de visualiser en un coup d'œil l'avancement global (via les jauges et l'indice d'écart) puis de descendre au niveau du détail (planning, phases, financier) selon le besoin, avec une page de questions-réponses en langage naturel pour les explorations ad hoc.

**Limites & pistes :** Le rapport repose sur des données rechargées manuellement à ce stade ; une industrialisation demanderait une source connectée en direct (ERP ou outil de gestion de projet) pour un suivi réellement temps réel. La carte Azure Maps et les seuils d'alerte gagneraient à être calibrés avec les chefs de projet utilisateurs finaux pour coller à leurs seuils de tolérance réels plutôt qu'à des paliers par défaut.

**Outils :** Power BI (DAX pour les indicateurs calculés dont l'indice d'écart, Power Query, Azure Maps, visuel Q&A en langage naturel)

**Lien GitHub :** [à compléter]
