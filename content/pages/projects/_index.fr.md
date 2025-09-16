+++
title = "Projets"
date = "2025-09-15T04:53:57+01:00"
author = "wolfiy"
keywords = ["projets", "développement"]
description = "Projets réalisés."
showFullContent = false
readingTime = true
hideComments = false
draft = false
+++

# Projets

Ces projets sont classés par ordre alphabétique.

## Anilist Badges

Quand j'ai rejoint la communauté Anilist, je suis tombé sur des événements organisés par différents groupes (AL-Badges, Kusogaki, AWC, ...), et j'ai décidé d'apporter ma contribution en créant un set de badges. Je n'ai pas prévu d'en faire de nouveaux, mais tous les badges ainsi que les fichiers `.psd` ont été archivés dans un dépôt Git. Sentez-vous libre de les réutiliser!

Archive: https://gitlab.com/wolfiy/alb/

## Automail

J'ai contribué au développement du script Automail pour Anilist (une collection d'améliorations et de traductions utilisateurs pour le site de *tracking*) en y ajoutant une traduction française.

Dépôt Git: https://github.com/hohMiyazawa/Automail

## Black Anilist

Le thème sombre d'Anilist étant bleu, j'ai décidé de créer mon propre style personnalisé. Ce *user style* permet à l'utilisateur de choisir une couleur d'accent, corrige bugs et inconsistances, et améliore certaines animations.

{{< image src="https://go.wolfiy.ch/assets/img/projects/black-al.png" alt="Thème Anilist sombre" position="center" style="width: 80%;" >}}

Dépôt Git: https://gitlab.com/wolfiy/anilist-black-theme

## Blog

Le site sur lequel vous vous trouvez est également un projet à part entière. Il a été réalisé à l'aide du programme Hugo, et complété d'un thème personnalisé tiré d'un projet existant appelé "Hugo Theme Terminal".

Dépôt Git du site: https://github.com/wolfiiy/momiko  
Dépôt Git du thème: https://github.com/wolfiiy/hugo-theme-momiko-terminal

## Edits

Lorsque j'étais plus jeune, j'ai réalisé quelques *edits* sur des jeux comme *Call of Duty*, ce qui m'a permis de me familiariser avec la suite *Adobe*. Une bonne partie est maintenant non répertoriée, mais tout peut être retrouvé dans une playlist dédiée.

Chaine: https://youtube.com/DarkWolfiiy  
Dernière vidéo: https://youtube.com/watch?v=XDFgXyqNPzk

## Homelab

Lors des confinements du COVID-19, j'ai décidé d'héberger un serveur *Mincraft* à l'aide d'un vieux PC pour jouer avec quelques amis. Ce qui a commencé par être un moyen d'économiser sur les frais d'hébergement s'est finalement transformer en un véritable *homelab*. A ce jour, quasiment tout le *hardware* que j'utilisais en 2020 a été remplacé.

{{< image src="https://go.wolfiy.ch/assets/img/projects/homeserver.png" alt="Dashboard de Proxmox" position="center" style="width: 80%;" >}}

Le serveur principal, sous Proxmox, est basé sur un Ryzen 9 5900x, 128 Gb de DDR4 ECC et un total d'un peu plus de 72 Tb de stockage en RAIDZ2. Le NAS est virtualisé, mais un contrôleur dédié (LSI 9201-8i) permet un accès direct aux disques sans aucune abstraction.

Ce serveur est utilisé pour toute une variété de services: médias, automation, moteur de recherche, cloud, backups, Minecraft, ...

## Javelo

Javelo est une application permettant de planifier des itinéraires à vélo sur le territoire suisse. Lorsqu'au moins deux points ont été ajoutés à la carte, le chemin le plus rapide et adapté aux cyclistes est trouvé, et une courbe permettant de visualiser le dénivelé s'affiche. Une fois générée, la route peut être exportée au format `.gpx`.

{{< image src="https://gitlab.com/wolfiy/wolfiy.gitlab.io/-/raw/master/assets/img/projects/javelo.png" alt="Affichage de Javelo" position="center" style="width: 70%;" >}}

Cette application a été réalisée à l'aide d'un ami lors de mon second semestre d'informatique à l'EPFL. Elle a été écrite en Java et l'interface est basée sur JavaFX.

Dépôt Git: https://gitlab.com/wolfiy/CS-108p

## Linktree

Ne voulant pas dépendre d'un service tiers, j'ai décidé de créer mon propre remplacement aux services de type "Linktree". La page s'adapte automatiquement au thème (clair ou sombre) du navigateur.

{{< image src="https://go.wolfiy.ch/assets/img/projects/linktree.png" alt="Page d'accueil du link tree" position="center" style="width: 75%;" >}}

Dépôt Git: https://gitlab.com/wolfiy/linktree  
Démo live: https://linktree.wolfiy.ch/

## Mastermind

Mastermind est un projet en deux parties réalisé au début de la formation d'informaticien à l'ETML. En première lieu, une version CLI a été créée afin de se familiariser avec les bases du C#. 

{{< image src="https://go.wolfiy.ch/assets/img/projects/mastermind.png" alt="Partie terminée de Mastermind (CLI)" position="center" style="width: 60%;" >}}

Quelques semaines plus tard, cette base a été reprise et portée sur Windows Form. La version GUI supporte différents thèmes, propose un mode debug, un mode triche et est localisée en plusieurs langues.

{{< image src="https://gitlab.com/wolfiy/etml-i404-mastermind-gui/-/raw/master/screenshots/won.PNG" alt="Partie terminée de Mastermind (GUI)" position="center" style="width: 20%;" >}}

Dépôt Git (CLI): https://gitlab.com/wolfiy/etml-i403-mastermind  
Dépôt Git (GUI): https://gitlab.com/wolfiy/etml-i404-mastermind-gui

## RATP

Dans ce projet réalisé à l'ETML, j'ai repensé l'interface utilisateur des automates à billets de la RATP, puis implémenté le nouveau design en C# (.NET 8) en utilisant Windows Forms.

{{< image src="https://go.wolfiy.ch/assets/img/projects/ticket-machine-redesign.png" alt="Interface de l'automate RATP" position="center" style="width: 60%;" >}}

L'application est localisée dans cinq langues. Le code suit le patron de conception MVC et suit les bonnes pratiques i18n.

Dépôt Git: https://gitlab.com/wolfiy/ticket-machine-redesign

## Sites web

L'ensemble des sites webs que j'ai réalisés sont *open source*.

{{< image src="https://go.wolfiy.ch/assets/img/projects/website.png" alt="Page d'accueil d'une ancienne version du site" position="center" style="width: 80%;" >}}

Site: https://go.wolfiy.ch/ ([α](https://go.wolfiy.ch/v1/index.html), [β](https://go.wolfiy.ch/v2/index.html))  
Blog: https://www.momiko.moe/fr

Dépôt Git (go.wolfiy.ch): https://gitlab.com/wolfiy/wolfiy.gitlab.io  
Dépôt Git (www\.momiko.moe): https://github.com/wolfiiy/momiko

## Spicy Invaders

Spicy Invaders est un clone du jeu *Space Invaders* réalisé en C# dans le cadre du cours de pratique de la programmation orientée objet à l'ETML. Nous avions beaucoup de liberté quant à l'implémentation et l'ajout de fonctionnalités.

{{< image src="https://go.wolfiy.ch/assets/img/projects/spicy-invaders.png" alt="Ecran de jeu de Spicy Invaders" position="center" style="width: 60%;" >}}

Ma version du jeu propose trois niveaux de difficultés, plusieurs types d'ennemis, du son ainsi qu'un *framerate* ajustable.

En termes d'implémentation, mon jeu suit le *design pattern* MVC. Il est très modulable (bonne séparation des objets, classes et interfaces). La librairie NAudio a été utilisée pour les sons et un installateur est fourni.

Dépôt Git: https://gitlab.com/wolfiy/spicy-invaders

## Start page

Il y a quelques années, j'ai commencé à *rice* mon OS. Voulant créer un visuel cohérent, j'ai créé ma propre *start page* pour mon navigateur. Elle a subi de nombreuses modifications depuis, mais elle reste relativement simple à mettre en place et à personnaliser.

{{< image src="https://gitlab.com/wolfiy/wolfiy.gitlab.io/-/raw/master/assets/img/projects/startpage.png" alt="Affichage de la start page" position="center" style="width: 80%;" >}}

Aujourd'hui, elle supporte les thèmes clair et sombre, et plusieurs images peuvent être utilisée.

Dépôt Git: https://gitlab.com/wolfiy/wlfys-minimal-startpage  
Démo live: https://start.wolfiy.ch/