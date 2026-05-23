---
title: Garmin bridge
date: 2026-05-21
draft: false
image: graphique.png
tags:
  - outils
  - IA
  - projet
---
Ça fait un peu plus d’un an que j’ai repris la course, d’abord pour la santé, puis l’idée de courir un semi-marathon s’est doucement installée… 
N’ayant aucune connaissance en performance de course à pied, j’ai tout naturellement été poser des questions à un LLM, à l’époque ChatGPT. 
* Objectif : courir un semi-marathon fin août.
* Méthode : il me donne mes séances de la semaine 
* Feed back: je lui envoie des screenshots de mes activités Garmin.

J’ai tenu un temps comme ça, couru mon semi-marathon mais ce fonctionnement devint très rapidement contraignant et plus compliqué que ce que j’étais prêt à faire quotidiennement. 
Je suis aussi tombé sur certains problème avec ce fonctionnement, par exemple la lecture d’une image par IA est un peu approximative, les données chiffrées sont estimées « à vue d’œil ».
Je cherche alors des solutions pour exporter plus de données, plus rapidement et sans les noyer dans une image. C’est là que je trouve [GarminDB](https://github.com/tcgoetz/GarminDB), un projet open source qui récupère les données Garmin et les sauvegarde localement dans des fichiers de bases de données.
Après avoir essayé et construit une API sommaire dessus, je me rends compte que ce n’est pas très adapté à mon IA. Je dois lui donner le lien pour accéder aux données à chaque fois. 
Ayant entendu parler de ce protocole de récupération de données conçu particulièrement pour les IA, je décide un an plus tard de mettre en place un serveur MCP tout aussi sommaire pour ma préparation au marathon 2026.
Voilà comment j’ai créé [Garmin-bridge](https://github.com/Nem0oo/garmin-bridge), le pont entre les IA et mes données Garmin. Je l’utilise quotidiennement, il a ses faiblesses, mais chaque fois qu’une donnée manque à mon IA, je lui ajoute un accès. L’API quant à elle me sert surtout pour partager facilement les stats d’une course avec des amis.

{{< img src="graphique.png" alt="Graphique brut généré par l'API" width="100%">}}
*Données brutes exportées via l'API*

{{< img src="analyse.png" alt="Analyse IA de la même course" width="100%">}}
*La même course analysée par l'IA grâce au MCP*
