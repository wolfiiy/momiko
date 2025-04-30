+++
title = "Configurer le clavier japonais sous Arch Linux"
date = "2025-04-10T19:29:48+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["linux", "japonais"]
keywords = ["arch", "linux", "clavier", "japonais"]
description = "Cet article décrit la procédure à effectuer afin de configurer un clavier japonais sur Arch Linux."
showFullContent = false
readingTime = true
hideComments = false
+++

## Prérequis

### Police

Par défaut, le système n'est pas muni de polices d'écritures japonaises, il est donc nécessaire d'en installer une afin de permettre un affichage correct des *kanas* et des *kanjis*.

Je recommande la police *Noto* car très complète et distribuée sous licence libre.

```bash
sudo pacman -S --needed noto-fonts noto-fonts-cjk
```

Le premier paquet installera la police "de base" contenant les caractères d'alphabets (latin, cyrillique, ...) et le second contient les idéogrammes (*kanji*, *hanzi*, *hanja*).

D'autres polices peuvent être trouvées sur le [wiki](https://wiki.archlinux.org/title/Localization/Japanese) d'*Arch Linux* ainsi que sur le [blog](https://tatsumoto-ren.github.io/blog/resources.html#fonts) de Tatsumoto Ren.

> Attention! Certains idéogrammes s'écrivent différemment en chinois et en japonais! Par exemple, le caractère `直` ne contient pas de trait vertical en chinois[^1].

[^1]: Wiktionary, *[直 - Alternative forms](https://en.wiktionary.org/wiki/%E7%9B%B4#Alternative_forms)* [en anglais]

### Locale japonaise

Les locales permettent au système d'effectuer le rendu des polices d'écriture et d'afficher les formats régionaux (monétaires, dates, heures, ...) spécifiques à une langue ou une région. Si une locale est manquante, certains textes pourraient ne pas s'afficher correctement[^2].

[^2]: Archwiki, *[Localization/Japanese](https://wiki.archlinux.org/title/Localization/Japanese)* [en anglais].

L'ajout d'une locale - quelle que soit la langue - se fait via le fichier `/etc/locale.gen`, utilisé comme référence lorsque le système génère ses locales. Pour ajouter la locale japonaise, décommenter la ligne `ja_JP.UTF8 UTF8` en supprimant le caractère `#`au début de celle-ci. Si d'autres locales sont activées, ne pas les supprimer.

```bash
sudo vim /etc/locale.gen
```

Le contenu du fichier devrait alors ressembler à cela:

```cfg
# Fichier: /etc/locale.gen
# ...
#iu_CA UTF-8  
#ja_JP.EUC-JP EUC-JP  
ja_JP.UTF-8 UTF-8  
#ka_GE.UTF-8 UTF-8  
#ka_GE GEORGIAN-PS
# ...
```

Une fois la ligne modifiée, sauvegarder le fichier et exécuter la génération des locales à l'aide de l'outil `locale-gen`.

```bash
sudo locale-gen
```

Enfin, pour vérifier l'activation de la locale, il est possible de lister l'ensemble des locales présentes sur le système à l'aide de la commande `locale -a`. Si ja_JP.utf8 s'y trouve, la manipulation est réussie.

Pour référence, voici la sortie obtenue sur mon sytème:

```txt
[akari@nyarch ~]$ locale -a
C
C.utf8
en_US.utf8
fr_CH.utf8
ja_JP.utf8
POSIX
```

## Installation et configuration du clavier

Un clavier japonais est constitué de deux éléments:

- Un input method framework (IMF) pour permettre à l'utilisateur de changer de IME.
- Un input method editor (IME) pour convertir les lettres latines en kanas et kanjis.

Sur les environnements basés sur GTK (GNOME, Mate, ...), il est courant de trouver l'IMF Ibus, alors que sur les environnements basés sur Qt (KDE Plasma, ...), Fctix5 est plus souvent utilisé. Les deux fonctionnent avec tous les IME.

Il existe de nombreux IME (cf. [wiki](https://wiki.archlinux.org/title/Localization/Japanese#Input_Method_Editor_%28IME%29)), mais le plus utilisé est mozc, un projet open source basé sur Google Japanese Input. Tous les paquets peuvent être installés depuis les répertoires officiels d'Arch Linux, à l’exception de `ibus-mozc` qui peut être trouvé sur les AUR.

```bash
# GTK
sudo pacman -S ibus
paru -S ibus-mozc
```

```bash
# Qt
sudo pacman -S fcitx5-im fcitx5-mozc
```

Ensuite, trois ou quatres variables d'environement doivent être ajoutées, selon l'IMF, ce qui peut se faire an ajoutant les lignes suivantes au fichier `~/.config/environment.d/envvars.conf`.

```cfg
# GTK
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
MOZC_IBUS_CANDIDATE_WINDOW=ibus
```

```cfg
# QT
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

A noter que les variables d'environnement pour fcitx ne contiennent pas de 5.

Enfin, le clavier peut être ajouté à la session. Sur mon système, basé sur GNOME, cela se fait via l'application Paramètres, sous *Clavier* > *Méthodes d'entrées* > *Ajouter une méthode d'entrée* > *Japonais*.