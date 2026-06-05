---
layout: default
nav_order: 4
title: Études et choix techniques
---

# Études et choix techniques

Pour la partie technique, on a décidé de partir sur une machine core XY. On trouvait que c'était la meilleure solution pour gérer les tracés du dessin. On a utilisé Onshape pour modéliser l'ensemble de la machine en 3D, histoire d'être sûrs de notre coup avant de fabriquer quoi que ce soit. Pour le matériel, on a pris une planche en bois qu'on a passée à la découpeuse laser. Ça nous a permis d'avoir une surface plate pour mettre la feuille .

Le choix d'une architecture en "H" vise avant tout à optimiser la répartition des contraintes mécaniques. Sur ce type d'équipement, l'inertie est la principale cause de perte de précision. En fixant les composants les plus denses (notamment les moteurs pas-à-pas) directement sur le cadre extérieur fixe, on allège drastiquement l'équipage mobile. Le châssis conserve ainsi sa rigidité et limite l'apparition de vibrations parasites.

Nous avons fais le choix de mettre deux barres sur l'axe X car il répond à un problème mécanique direct : la gestion du couple de renversement. Le frottement continu du stylo sur la surface de tracé génère une force de levier. Sur un axe à barre unique, cette force provoquerait un pivotement ou un tremblement du chariot. L'ajout d'une seconde barre parallèle permet de contraindre ce degré de liberté en rotation. Le porte-outil est ainsi maintenu strictement perpendiculaire au plan de travail, ce qui garantit une pression d'appui constante et une régularité parfaite du trait.

Le choix de la transmission s'est porté sur un système à double courroie, qui constitue le cœur même de la cinématique CoreXY. Plutôt que de séparer mécaniquement les axes X et Y en attribuant un moteur à chacun, ce montage exploite deux courroies distinctes qui relient les moteurs fixes au chariot central. Le principe mécanique est particulièrement élégant : c'est le travail combiné des deux moteurs qui dicte le déplacement de l'outil. Lorsqu'ils tournent dans le même sens, le chariot avance sur un axe ; lorsqu'ils tournent en sens opposé, il se déplace sur l'axe perpendiculaire. Le véritable atout de cette conception réside dans la symétrie des forces. Le chariot central est constamment "tenu" par les courroies, ce qui permet de réduire considérablement les jeux mécaniques. En répartissant l'effort de traction sur les deux boucles à la fois, la machine gagne énormément en fluidité, un critère indispensable pour garantir la netteté et la précision du tracé final.

La machine a été pensée avec une symétrie parfaite de part et d'autre de l'axe X : la partie située au-dessus de l'axe est l'exacte réplique de celle située en dessous. Ce choix de conception nous a fait gagner un temps précieux, puisqu'il a suffi de réfléchir et de modéliser une seule moitié de la structure avant de la dupliquer. Au-delà de ce gain de temps évident, cette symétrie bilatérale rend la machine visuellement beaucoup plus belle et équilibrée.



# Code

Afin de rendre le fonctionnement de notre programme plus visuel et compréhensible, l'algorigramme ci-dessous détaille le cycle de décision principal de la carte Arduino. Plutôt que d'exposer des lignes de code complexes, ce schéma se concentre sur l'essentiel : la logique d'exécution de la machine. Il décrit étape par étape comment le "cerveau" du traceur réceptionne une ligne de G-code, l'analyse, puis la traduit instantanément en actions mécaniques concrètes, qu'il s'agisse d'actionner le servomoteur pour manipuler le stylo, ou de calculer les coordonnées pour déplacer le chariot. Il résume ainsi la boucle fondamentale qui permet de passer du fichier numérique au dessin physique.

![Image Algo](/images/algorigramme.png)

Nous avons également un script Python qui convertit l'image en G-code en appliquant une succession de traitements mathématiques. Dans un premier temps, l'image est simplifiée en noir et blanc (binarisation) afin d'en extraire les contours sous forme de coordonnées géométriques. Ces trajectoires sont ensuite traduites en instructions physiques précises (levée, descente et déplacement du stylo). L'efficacité de ce processus repose sur l'interpolation vectorielle : n'ayant aucune vision globale du dessin final, la machine exécute rigoureusement une séquence de "points à relier". En découpant les courbes complexes en une multitude de petits segments rectilignes successifs, le système permet aux moteurs mécaniques de restituer des trajectoires fluides et de reproduire fidèlement l'élégance du tracé original.

# FluidNC et UGS

Au début du projet, nous utilisions une carte classique (une Arduino) avec le logiciel UGS. C'était un très bon point de départ, mais cela nous obligeait à garder l'ordinateur branché en permanence avec un câble pour envoyer le dessin à la machine. De plus, à chaque fois que nous voulions changer un petit réglage mécanique, il fallait modifier et réinstaller un code informatique assez complexe. Pour rendre le projet plus moderne et pratique, nous avons donc décidé de remplacer l'Arduino par une petite carte beaucoup plus puissante : l'ESP32.

L'avantage majeur de cette nouvelle carte est sa simplicité de configuration : il n'y a plus besoin de programmer ou de réinstaller du code complexe. L'intégralité des réglages de la machine s'effectue simplement en éditant un petit fichier texte que l'on dépose dans la mémoire de la carte. De plus, grâce au Wi-Fi intégré, la machine possède sa propre interface web. On peut s'y connecter directement depuis un simple navigateur internet pour contrôler la machine, envoyer les fichiers de dessin et lancer les tracés entièrement sans fil, ce qui est très pratique.


