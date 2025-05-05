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

Depuis cette page, un bouton devrait permettre de créer de nouveaux enregistrements DNS et / ou de directement modifier les *zonefiles*.

### Enregistrements DNS

Imaginons que le domaine à utiliser soit `exemple.ch`, et que l'on veuille lier un serveur *Minecraft* au sous-domaine `mc.exemple.ch`. Deux enregistrements seront alors nécessaires:

1. Un enregistrement de type `A` pour faire correspondre le (sous-)domaine à l'adresse IP du serveur hébergeant l'instance de *Minecraft*.
2. Un enregistrement de type `SRV` afin de préciser aux serveurs DNS qu'il s'agit de "trafic *Minecraft*".

> Dans le cadre d'un serveur auto-hébergé (*selfhost*), il est vivement conseillé de mettre en place un DDNS et de remplacer l'enregistrement de type `A` par un `CNAME` pointant vers le DDNS.

#### A

D'abord, ajouter un enregistrement de type `A`:

- Type: `A`
- Source: `mc` (sous-domaine à utiliser, ce qui donnera ici `mc.exemple.ch`)
- Target: `aaa.bbb.ccc.ddd` (adresse IP publique du serveur *Minecraft*)
- TTL: `300` (5 mins)

Si le serveur est doté d'une adresse IPv6, il est possible d'effectuer la même procédure en choisissant un enregistrement de type `AAAA`.

{{< figure src="/images/posts/minecraft-server-domain/a-record.png" alt="Paramètrage de l'enregistrement de type A." position="center" caption="Création de l'enregistrement de type A." captionPosition="center">}}

#### SRV

Ensuite, créer un enregistrement de type `SRV` paramétré ainsi:

- Type: `SRV`
- Service: Minecraft
- Protocol: `tcp.mc` (`tcp.` suivi du sous-domaine défini précédemment)
- Weight: 5
- Port: `25565` (ou autre si le port à été changé dans le `server.properties`)
- Target: `mc.example.ch` (selon ce qui a été défini précédemment)
- TTL: 5 mins
- Priority: 10

{{< figure src="/images/posts/minecraft-server-domain/srv-record.png" alt="Paramètrage de l'enregistrement de type SRV." position="center" caption="Création de l'enregistrement de type SRV." captionPosition="center">}}

#### Cas spécifique: *selfhost*
