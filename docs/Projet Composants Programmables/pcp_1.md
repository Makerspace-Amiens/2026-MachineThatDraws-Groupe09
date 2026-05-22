---
layout: default
title: Kicad
parent: Projet composants
nav_order: 1
---
Ce projet s’inscrit dans la continuité du projet Machine that draws que vous avez réalisé précédemment. L’objectif est de concevoir et fabriquer une carte électronique dédiée pour remplacer le contrôleur de drivers.

La carte intégrera :

- ESP32 comme microcontrôleur principal
- 2 drivers A4988 pour piloter les moteurs pas-à-pas X et Y
- Lecteur de carte SD pour stocker les fichiers G-code ou dessins
- Écran OLED pour afficher l’état, les menus et la progression
- Connecteurs pour moteurs, alimentation et extension
- Gestion des alimentations

PCB de la carte:

![Imagepcb](images/Capture d’écran 2026-05-22 à 13.40.58.png)

Voici le test de l'écran:

<video width="100%" height="100%" controls>
        <source src="images/videotestecrans.MOV" type="videotestecrans/MOV" />
</video>


