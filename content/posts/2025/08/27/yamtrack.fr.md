+++
title = "Présentation et installation de Yamtrack"
date = "2025-08-27T20:38:56+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["self-host", "docker"]
keywords = ["self-host", "docker", "tracking", "suivi", "yamtrack"]
description = "Présentation du service de gestion de collections de médias Yamtrack."
showFullContent = false
readingTime = true
hideComments = false
draft = false
+++

## Présentation

Si vous êtes un avide utilisateur des services de gestion de collections tels qu'*[Anilist](https://anilist.co/)*, *[Trakt](https://trakt.tv/)*, *[Simkl](https://simkl.com/)* ou *[GoodReads](https://www.goodreads.com/)*, l'application *[Yamtrack](https://github.com/FuzzyGrim/Yamtrack)* risque de fortement susciter votre curiosité.

En effet, *Yamtrack* est un service auto-hébergé permettant de regrouper les
fonctionnalités de ces différents sites. Depuis cette application, il est
possible de *tracker* les séries, films, anime, livres et même jeux vidéo
complétés ou en cours de visionnage/lecture/jeu. Il permet aussi de noter les
entrées, de créer et gérer des collections de média, de visualiser des
statistiques et propose un calendrier facilitant le suivi des sorties. 

Des options d'importation de données sont disponibles, facilitant ainsi la migration
depuis des plateformes célèbres[^1]. Malheureusement, cette application ne permet
pas encore le suivi de musique comme
*[RateYourMusic](https://rateyourmusic.com/)* le propose.

[^1]: L'import est possible depuis *Trakt*, *Simkl*, *MyAnimeList*, *Anilist*, *Kitsu*, *HowLongToBeat* et une autre instance de *Yamtrack*.

Afin de vous faire une meilleure idée de son fonctionnement, une démo est mise à disposition par son développeur, FuzzyGrim, [ici](https://yamtrack.fuzzygrim.com/). Les identifiants sont `demo` et `demo`.

Pour directement passer à l'installation, cliquer [ici](#installation).

## Utilisation

La page d'accueil de l'application permet de visualiser l'ensemble des oeuvres
en progression. Les petits boutons `+` et `-` situés sous le titre des entrées permettent de rapidement modifier la progression d'une série.

{{< figure src="/images/posts/2025/08/27/yamtrack/home.png" alt="Page d'accueil de Yamtrack." position="center" caption="Page d'accueil de Yamtrack." captionPosition="center">}}

### Gestion d'entrées

Pour rechercher une oeuvre, il suffit d'entrer son titre dans la barre de
recherche supérieure. Attention à sélectionner le bon type de média afin de
s'assurer de trouver le bon résultat!

{{< figure src="/images/posts/2025/08/27/yamtrack/search.png" alt="Résultats de recherche." position="center" caption="Résultats de recherche." captionPosition="center">}}

La page d'une oeuvre permet d'en afficher les détails: titre complet, genres,
format, état de diffusion, date de sortie, studios associés, ... 

On y trouve également un résumé, plus ou moins long, une liste des saisons (si applicable), ainsi qu'une liste d'oeuvres recommandées.

{{< figure src="/images/posts/2025/08/27/yamtrack/details.png" alt="Détails d'une oeuvre." position="center" caption="Détails d'une oeuvre." captionPosition="center">}}

Dans le cas d'une série ou d'un anime, il est possible d'afficher la liste des épisodes d'une certaine saison en cliquant sur cette dernière, depuis la liste visible sur la capture d'écran précédente.

{{< figure src="/images/posts/2025/08/27/yamtrack/season.png" alt="Affichage d'une saison." position="center" caption="Affichage d'une saison." captionPosition="center">}}

Depuis cette vue, un épisode peut être marqué comme étant visionné en cliquant sur le bouton bleu-violet contenant une icône d'oeil.

Une entrée (film, série, saison, jeu, livre) peut être éditée à l'aide du bouton "Add to tracker", qui ouvre un pop-up permettant d'en définir le statut, d'y ajouter une note ("Score") et un mémo ("Note").

{{< figure src="/images/posts/2025/08/27/yamtrack/add.png" alt="Ajout d'une entrée." position="center" caption="Ajout d'une entrée." captionPosition="center">}}

### Affichage des entrées

Enfin, les menus listés sur la barre de navigation latérale, à gauche de l'écran, permettent d'accéder à une liste familière aux utilisateurs des plateformes populaires précédemment citées.

{{< figure src="/images/posts/2025/08/27/yamtrack/list.png" alt="Liste d'entrées." position="center" caption="Liste d'entrées." captionPosition="center">}}

### Fonctions avancées

Le menu "Statistics" donne accès à des graphiques générés à partir des entrées ajoutées depuis le compte de l'utilisateur.

{{< figure src="/images/posts/2025/08/27/yamtrack/stats.png" alt="Exemples de statistiques." position="center" caption="Exemples de statistiques." captionPosition="center">}}

"Calendar" permet d'afficher un calendrier des sorties. *Yamtrack* propose également un lien permettant d'importer celui-ci dans des applications tierces.

{{< figure src="/images/posts/2025/08/27/yamtrack/calendar.png" alt="Calendrier." position="center" caption="Calendrier." captionPosition="center">}}

Les entrées peuvent être exportées depuis les paramètres ("Settings"), sous "Export data". Cet export est réalisé au format CSV.

{{< figure src="/images/posts/2025/08/27/yamtrack/export.png" alt="Export des données." position="center" caption="Export des données." captionPosition="center">}}

Des données existantes peuvent être importées depuis les paramètres, sous "Import data". Pour *Trakt*, *MAL*, *Anilist* et *Kitsu*, il suffit d'entrer le nom d'utilisateur correspondant. Pour *Simkl*, il est nécessaire de s'identifier via le bouton "Connect with Simkl".

*Yamtrack* et *HowLongToBeat* requièrent une sauvegarde au format CSV.

Les imports peuvent être réalisés de manière périodique en modifiant les valeurs le champ "Import frequency". Le champ "Import mode" permet de définir s'il faut écraser les données existantes ("Sync new items and overwrite existing") ou non ("Only sync new items").

{{< figure src="/images/posts/2025/08/27/yamtrack/import.png" alt="Import des données." position="center" caption="Import des données." captionPosition="center">}}

Des entrées et des listes personnalisées peuvent être ajoutées respectivement depuis les menus "Create custom" et "Lists". Les premières sont utiles dans le cas où une oeuvre ne serait pas trouvable dans les bases de données utilisées par *Yamtrack*, et les secondes permettent de grouper des oeuvres et de partager ces groupes à d'autres utilisateurs de l'instance.

Enfin, des intégrations à *Jellyfin*, *Emby* et *Plex* peuvent être configurées depuis les paramètres, sous "Integrations". Des instructions détaillées y sont présentes.

## Installation

*Yamtrack* peut être aisément déployé à l'aide d'un conteneur *Docker*. Il repose sur une base de données *Redis*. Personnellement, j'ai configuré mon instance comme suit. La base de données y est également créée.

```yaml
services:
  yamtrack:
    container_name: yamtrack
    image: ghcr.io/fuzzygrim/yamtrack
    restart: unless-stopped
    depends_on:
      - redis
    environment:
      - SECRET=${SECRET}
      - REDIS_URL=${REDIS_URL}      
      - DB_HOST=${DB_HOST}
      - DB_NAME=${DB_NAME}
      - DB_USER=${DB_USER}
      - DB_PASSWORD=${DB_PASSWORD}
      - DB_PORT=${DB_PORT}
      - MAL_NSFW=true
      - MU_NSFW=true
      - IGDB_NSFW=true
      - URLS=https://***.***, https://***.***
      - TZ=Europe/Zurich
    ports:
      - "***:8000"

  redis:
    container_name: yamtrack-redis
    image: redis:7-alpine
    restart: unless-stopped
    volumes:
      - ./redis_data:/data
```

Pour masquer les images choquantes, les variables `MAL_NSFW`, `MU_NSFW` et `IGDB_NSFW` peuvent être définies sur `false`.

Les valeurs renseignées au format `${VALEUR}` sont contenues dans un fichier nommé `.env` situé juste à côté du *compose file*, peuplé ainsi:

```env
SECRET=***
REDIS_URL=redis://redis:6379
DB_HOST=***
DB_PORT=***
DB_NAME=***
DB_USER=***
DB_PASSWORD=***
```

Pour des raisons de confidentialité, certaines valeurs ont été offusquées et remplacées par la chaine `***`. Ces valeurs sont à adapter selon vos préférences et votre infrastructure.

Le conteneur peut ensuite être démarré et, l'application est accessible via la paire adresse IP de l'hôte et port défini sous `ports` dans le fichier `docker-compose.yml`. 

{{< figure src="/images/posts/2025/08/27/yamtrack/login.png" alt="Formulaire de connexion." position="center" caption="Formulaire de connexion." captionPosition="center">}}

Par défaut, aucun compte n'existe; il faut alors cliquer sur "Register now" afin d'en créer un.

{{< figure src="/images/posts/2025/08/27/yamtrack/signup.png" alt="Formulaire de création de compte." position="center" caption="Formulaire de création de compte." captionPosition="center">}}