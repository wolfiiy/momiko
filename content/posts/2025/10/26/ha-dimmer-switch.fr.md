+++
title = "Configurer un Philips Hue Dimmer Switch sur Home Assistant"
date = "2025-10-26T17:16:56+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["self-host", "home assistant", "smart home"]
keywords = ["self-host", "home assistant", "lumière", "philips hue", "bouton", "scène"]
description = "Configuration d'un Hue Dimmer Switch sur Home Assistant afin de répliquer le comportement de base avec l'application officielle."
showFullContent = false
readingTime = true
hideComments = false
draft = true
+++

## Introduction

Il y a de cela déjà quelques années, je me suis procuré un kit de démarrage *Philips Hue*: quelques ampoules, un *bridge*, un variateur et une bande LED. Depuis 2020, j'ai commencé à sérieusement m'intéresser au *self-hosting* (auto-hébergement); c'est alors tout naturellement qu'un jour, j'ai décidé de configurer une instance de *Home Assistant* (HA).

Dans la vaste majorité des cas, je contrôle mes lumières à l'aide de raccourcis sur mon téléphones ou via des automations, et l'interrupteur n'est que rarement utilisé. Cependant, la possibilité de passer d'une scène à l'autre depuis l'interrupteur reste une fonctionnalité qui peut être utile de temps en temps, en particulier lorsque d'autres personnes souhaitent interagir avec les lumières sans passer par HA.

Dans cet article, je vais détailler la procédure à suivre pour restaurer le fonctionnement "par défaut" du *Hue Dimmer Switch*, c'est à dire:

- Presser une fois le bouton "On" pour activer une certaine scène;
- Presser successivement le bouton "On" pour passer à d'autres scènes;
- Presser une fois sur le bouton "Off" pour éteindre les lumières;
- Presser sur les boutons du milieu pour faire varier l'intensité de la lumière.

## Prérequis et conseils

Cet article part du principe qu'une instance de *Home Assistant* a été préalablement installée et correctement configurée; il ne détaille pas le déploiement de HA ni la configuration de l'intégration *Philips Hue*.

Pour se simplifier la vie, il est possible de créer des groupes de lampes en passant par *Settings*, *Devices & services*, *Helpers*, *Create helper* et en sélectionnant le type *Group* puis *Light group*. Ce n'est pas obligatoire, mais cela permet d'éviter de devoir ajouter manuellement chaque ampoule à chaque scène.

### Créer une scène

Les scènes peuvent être créées depuis *Settings*, *Automations & scenes*, *Scenes*. En cliquant sur le bouton *Create scene*, une page permettant de la paramétrer s'ouvre:

{{< figure src="/images/posts/2025/10/26/ha-dimmer-switch/scene-creation.png" alt="Formulaire de création d'une scène Home Assistant." position="center" caption="Création d'une scène." captionPosition="center">}}

Dans cet exemple, je crée une scène intitulée "Lumières éteintes". Comme j'ai préalablement créé un groupe appelé "Bedroom lights", j'ajoute cette *entity* et non chaque ampoule individuellement (ce qui se ferait sous *devices*). 

La couleur et l'intensité de chaque ampoule peuvent être configurées en cliquant sur l'icône à gauche du nom du groupe ou, le cas échéant, de la lampe.

{{< figure src="/images/posts/2025/10/26/ha-dimmer-switch/scene-lights.png" alt="Changement de l'intensité des lumières." position="center" caption="Changement de l'intensité des lumières." captionPosition="center">}}

Ici, j'ai choisi une couleur plutôt chaude et une intensité réduite. Au total, j'ai créé trois scènes: lumières allumées, lumières tamisées et lumières éteintes.

### Créer un script

Les scripts permettent de définir des séquences d'actions qui peuvent être exécutées par des automatisations ou depuis un raccourci (bouton virtuel, widget, etc.), et qui peuvent être réutilisées. Concrètement, dans mon cas, j'ai défini un script permettant d'éteindre la lumière qui est appelé en pressant sur l'interrupteur et lorsque je quitte mon domicile. Ainsi, la séquence d'action à exécuter n'a été définie qu'une seule fois. 

Un script peut être créé depuis *Settings*, *Automations & scenes* sous l'onglet *Scripts*, puis en cliquant sur le bouton *Create script*.

## Mise en place

### Bouton "On"


### Bouton "Off"

Premièrement, créer un nouveau script et choisir l'action *Scene 'Activate'*.

{{< figure src="/images/posts/2025/10/26/ha-dimmer-switch/script-action.png" alt="Choix de l'action à exécuter." position="center" caption="Choix de l'action à exécuter." captionPosition="center">}}

Puis, choisir la scène représentant la pièce avec les lumières éteintes (*Choose entity*) et sauvegarder.

{{< figure src="/images/posts/2025/10/26/ha-dimmer-switch/script-action-off.png" alt="Choix de l'action à exécuter." position="center" caption="Choix de l'action à exécuter." captionPosition="center">}}

Depuis *Settings*, *Automations & scenes*, sous l'onglet *Automations*, cliquer sur le bouton *Create automation* et choisir *Create new automation*.

Cette fois, le *trigger* est le quatrième bouton du variateur, et une fois pressé, le script permettant d'éteindre la lumière doit être exécuté.

{{< figure src="/images/posts/2025/10/26/ha-dimmer-switch/automation-off.png" alt="Automatisation permettant d'éteindre la lumière." position="center" caption="Automatisation permettant d'éteindre la lumière." captionPosition="center">}}

La condition que j'ai ajoutée peut être à ignorée ici aussi.

### Régler l'intensité