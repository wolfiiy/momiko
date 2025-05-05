+++
title = "Ajouter un nom de domaine à un serveur Minecraft"
date = "2025-05-05T08:55:12+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["réseau"]
keywords = ["domaine", "Minecraft"]
description = "Cet article explique comment ajouter un nom de domaine à un serveur Minecraft."
showFullContent = false
readingTime = true
hideComments = false
draft = true
+++

## Pourquoi?

Une fois le serveur *Minecraft* créé, il est possible de s'y connecter via son adresse IP. Cependant, celle-ci peut être compliquée à retenir ou à partager. Lier son serveur à un nom de domaine permet ainsi de créer une méthode d'accès personnalisée et facile à retenir.

> Attention! Cet article part du principe que le serveur *Minecraft* est déjà en place et fonctionnel.

## Mise en place

La première chose à faire est de se munir d'un nom de domaine. Ceux-ci peuvent être achetés auprès d'un *registrar* comme *[Infomaniak](https://www.infomaniak.com/en/domains)* ou *[Cloudflare](https://www.cloudflare.com/products/registrar/)*.

Le choix du *registrar* n'est pas important; les interfaces graphiques et les prix peuvent varier, mais les principes sont les même pour tous.

### Accès à la zone DNS

La zone DNS permet de configurer le nom de domaine (i.e. créer des sous domaine, lier des services, etc.).

Selon le *registrar*, l'accès à la zone DNS peut être différent. Dans mon cas, avec un domaine enregistré chez *Infomaniak*, il faut passer par la page de gestion (le "Manager"), sélectionner *Domain* sous *Web & Domains*, choisir le domaine à configurer puis, finalement, cliquer sur *DNS Zone* dans la barre latérale gauche.

### Enregistrements DNS

Imaginons que le domaine à utiliser soit `exemple.ch`, et que l'on veuille lier un serveur *Minecraft* au sous-domaine `mc.exemple.ch`.

#### Serveur hébergé

Dans le cas d'un serveur hégergé chez un tiers, deux enregistrements devront être créés:

1. Un enregistrement de type `A` pour aire correspondre le (sous-)domaine à l'adresse IP du serveur hébergant l'instance de *Minecraft*.
2. Un enregistrement de type `SRV` afin de préciser au serveurs DNS qu'il s'agit de "trafic *Minecraft*".

Depuis l'éditeur de zone DNS du *registrar*, créer un nouvel enregistrement de type `A`. La source sera le sous-domaine (p.ex. `mc.`), et la cible doit contenir l'adresse IP du serveur *Minecraft*.

{{< figure src="/images/posts/minecraft-server-domain/a-record.png" alt="Paramètrage de l'enregistrement de type A." position="center" caption="Création de l'enregistrement de type A." captionPosition="center">}}

Ensuite, créer un enregistrement de type `SRV`. La procédure est la même, mais il y a quelques paramètres supplémentaires à spécifier:

- 