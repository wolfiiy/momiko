+++
title = "Projets"
date = "2025-09-15T04:53:57+01:00"
author = "wolfiy"
keywords = ["projets", "développement"]
description = "Projects I made."
showFullContent = false
readingTime = true
hideComments = false
draft = false
+++

# Projects

These projects are sorted in alphabetical order.

## Anilist Badges

Upon joining the Anilist community, I came across events organized by various groups of users (AL-Badges, Kusogaki, AWC, etc.), and I decided to contribute by creating a set of badges. I probably won't be making any more badges, but if you like the design, feel free to use the `.psd` files provided in the archive below.

Link: [Archive](https://gitlab.com/wolfiy/alb/)

## Automail

I helped translate the Automail script for Anilist—(a collection of enhancements and user-made translations for the tracking website—to French.

Link: [Repository](https://github.com/hohMiyazawa/Automail)

## Black Anilist

The default dark theme of Anilist leaning towards a blue tint, I decided to write my own "true" dark theme. This userstyle also lets the user choose a custom accent color, fixes a few bugs and design inconsistencies, and adds a few animations.

{{< image src="https://go.wolfiy.ch/assets/img/projects/black-al.png" alt="Black Anilist showcase" position="center" style="width: 80%;" >}}

Link: [Repository](https://gitlab.com/wolfiy/anilist-black-theme)

## Blog

The website you are reading this from is a project in itself. It has been built using the Hugo SSG, on which I applied my own theme, forked from "Hugo Theme Terminal".

Links: [Git (site)](https://github.com/wolfiiy/momiko) | [Git (theme)](https://github.com/wolfiiy/hugo-theme-momiko-terminal)

## Edits

Back when I was in middle and high school, I made a few edits on games like "Call of Duty". This allowed me to get familiar with the *Adobe* suite. The better part of my edits is is now unlisted, but everything can be found in a dedicated playlist on my YouTube channel.

Links: [Channel](https://youtube.com/DarkWolfiiy) | [Last edit](https://youtube.com/watch?v=XDFgXyqNPzk)

## Homelab

During the COVID-19 lockdowns, I decided to self host my own *Minecraft* server on an old computer to play with a few friends. What began as a way to save some money on hosting turned into a fully fledged homelab. Nowadays, most of the hardware I was using in 2020 has been replaced.

{{< image src="https://go.wolfiy.ch/assets/img/projects/homeserver.png" alt="Proxmox dashboard" position="center" style="width: 80%;" >}}

The main server runs Proxmox and is built around a Ryzen 9 5900X, 128 GB of ECC DDR4, and roughly 72 TB of RAIDZ2 storage. The NAS has been virtualized, but a dedicated controller (LSI 9201-8i) is passed through, giving the VM full, direct access to the disks.

This server is used for a wide variety of purposes, including media, automation, search engine, cloud services, backups, *Minecraft*, and more.

## Javelo

Javelo is an application for planning bicycle trips throughout Switzerland. When at least two pins have been added to the map, the best route is calculated and a pop up window gives details about the elevation. The route can be exported as a `.gpx` file.

{{< image src="https://gitlab.com/wolfiy/wolfiy.gitlab.io/-/raw/master/assets/img/projects/javelo.png" alt="Javelo main window" position="center" style="width: 70%;" >}}

This program has been written with the help of a friend during our second semester of computer science at EPFL. It has been developped in Java, and the UI was built using JavaFX.

Link: [Repository](https://gitlab.com/wolfiy/CS-108p)

## Linktree

Not wanting to rely on third party services, I decided to write my own alternative to services such as *LinkTree*. It is easy to modify and follows the system theme (light & dark).

{{< image src="https://go.wolfiy.ch/assets/img/projects/linktree.png" alt="Linktree example" position="center" style="width: 75%;" >}}

Links: [Git](https://gitlab.com/wolfiy/linktree) | [Demo](https://linktree.wolfiy.ch/)

## Mastermind

Mastermind is a two-parts project I created at ETML. First, a CLI version of the board game was developed to practice the fundamentals of the C# programming language.

{{< image src="https://go.wolfiy.ch/assets/img/projects/mastermind.png" alt="End game screen of Mastermind (CLI)" position="center" style="width: 60%;" >}}

Then, a few weeks later, this base has been ported to Windows Form. The GUI version adds a graphical interface, multiple color palettes, a debug mode, a cheating mode, and a couple translations.

{{< image src="https://gitlab.com/wolfiy/etml-i404-mastermind-gui/-/raw/master/screenshots/won.PNG" alt="End game screen of Mastermind (GUI)" position="center" style="width: 20%;" >}}

Links: [Repository (CLI)](https://gitlab.com/wolfiy/etml-i403-mastermind) | [Repository (GUI)](https://gitlab.com/wolfiy/etml-i404-mastermind-gui)

## RATP

Dans ce projet réalisé à l'ETML, j'ai repensé l'interface utilisateur des automates à billets de la RATP, puis implémenté le nouveau design en C# (.NET 8) en utilisant Windows Forms.

{{< image src="https://go.wolfiy.ch/assets/img/projects/ticket-machine-redesign.png" alt="Interface de l'automate RATP" position="center" style="width: 60%;" >}}

L'application est localisée dans cinq langues. Le code suit le patron de conception MVC et suit les bonnes pratiques i18n.

Lien: [Git](https://gitlab.com/wolfiy/ticket-machine-redesign)

## Sites web

L'ensemble des sites webs que j'ai réalisés sont *open source*.

{{< image src="https://go.wolfiy.ch/assets/img/projects/website.png" alt="Page d'accueil d'une ancienne version du site" position="center" style="width: 80%;" >}}

Démo: [Site](https://go.wolfiy.ch/) ([α](https://go.wolfiy.ch/v1/index.html), [β](https://go.wolfiy.ch/v2/index.html)) | [Blog](https://www.momiko.moe/fr)  
Git: [Site](https://gitlab.com/wolfiy/wolfiy.gitlab.io) | [Blog](https://github.com/wolfiiy/momiko)

## Spicy Invaders

Spicy Invaders est un clone du jeu *Space Invaders* réalisé en C# dans le cadre du cours de pratique de la programmation orientée objet à l'ETML. Nous avions beaucoup de liberté quant à l'implémentation et l'ajout de fonctionnalités.

{{< image src="https://go.wolfiy.ch/assets/img/projects/spicy-invaders.png" alt="Ecran de jeu de Spicy Invaders" position="center" style="width: 60%;" >}}

Ma version du jeu propose trois niveaux de difficultés, plusieurs types d'ennemis, du son ainsi qu'un *framerate* ajustable.

En termes d'implémentation, mon jeu suit le *design pattern* MVC. Il est très modulable (bonne séparation des objets, classes et interfaces). La librairie NAudio a été utilisée pour les sons et un installateur est fourni.

Lien: [Git](https://gitlab.com/wolfiy/spicy-invaders)

## Start page

Il y a quelques années, j'ai commencé à *rice* mon OS. Voulant créer un visuel cohérent, j'ai créé ma propre *start page* pour mon navigateur. Elle a subi de nombreuses modifications depuis, mais elle reste relativement simple à mettre en place et à personnaliser.

{{< image src="https://gitlab.com/wolfiy/wolfiy.gitlab.io/-/raw/master/assets/img/projects/startpage.png" alt="Affichage de la start page" position="center" style="width: 80%;" >}}

Aujourd'hui, elle supporte les thèmes clair et sombre, et plusieurs images peuvent être utilisée.

Liens: [Git](https://gitlab.com/wolfiy/wlfys-minimal-startpage) | [Démo](https://start.wolfiy.ch/)