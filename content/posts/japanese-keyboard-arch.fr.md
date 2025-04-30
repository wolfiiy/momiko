+++
title = "Configurer le clavier japonais sous Arch Linux"
date = "2025-04-10T19:29:48+02:00"
lastmod = "2025-04-30T11:05:48+02:00"
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

## Clavier japonais

### Présentation

Un clavier japonais est constitué de deux éléments:

- Un *input method editor* (IME) pour convertir les caractères latins en *kanas* et *kanjis*.
- Un *input method framework* (IMF) pour permettre à l'utilisateur de changer d'IME.

Il existe deux IMF: [IBus](https://wiki.archlinux.org/title/IBus) et [Fctix5](https://wiki.archlinux.org/title/Fcitx5). Le premier est plus courant sur les environnements GTK comme GNOME ou Mate, alors que le second est plutôt utilisé dans les environnements Qt tels que KDE Plasma ou LXQt. Les deux sont compatibles avec l'ensembles des IME.

L'IME le plus souvent recommandé[^3] semble être [mozc](https://github.com/google/mozc); c'est aussi celui que j'utilise. Il s'agit d'un projet *open source* basé sur *Google Japanese Input*.

[^3]: Une liste des alternatives est disponible sur le wiki: Archwiki, *[IME](https://wiki.archlinux.org/title/Localization/Japanese#Input_Method_Editor_%28IME%29)* [en anglais]

### GTK

Dans un environnement GTK, il faut donc installer les paquets `ibus` et `ibus-mozc`. A noter que le premier se trouve dans les répertoires officiels d'*Arch Linux* alors que le second doit être récupéré depuis les *Arch User Repositories*.

```bash
sudo pacman -S ibus
paru -S ibus-mozc
```

Ensuite, quatre variables d'environnement doivent être ajoutées. Cela peut être fait en ajoutant les lignes suivantes au fichier `~/.config/environment.d/envvars.conf` (peut être créé si inexistant).

```cfg
# Fichier $HOME/.config/environment.d/envvars.conf
# /!\ Uniquement pour les sessions Wayland /!\
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
MOZC_IBUS_CANDIDATE_WINDOW=ibus
```

### Qt

Dans un environnement Qt, les paquets `fcitx5-im` et `fcitx5-mozc` doivent être installés. Ils sont tous deux accessibles depuis les répertoires officiels.

```bash
sudo pacman -S fcitx5-im fcitx5-mozc
```

Pour Fcitx5, seules trois variables d'environnement doivent être ajoutées. Celles-ci peuvent également être ajoutées, par exemple au fichier `~/.config/environment.d/envvars.conf`, qui peut être créé s'il n'existe pas.

```cfg
# Fichier $HOME/.config/environment.d/envvars.conf
# /!\ Uniquement pour les sessions Wayland /!\
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

Attention, les variables d'environnement pour Fcitx ne contiennent pas de "5"!

### Utilisation

Une fois que tout a été installé et configuré, le clavier japonais peut être utilisé.

L'ajout du clavier diffère selon l'environnement de bureau ou le *window manager* / *compositor* utilisé. Sur mon système, basé sur GNOME, il suffit d'ouvrir l'application *Paramètres* et d'accéder aux options du clavier.

{{< figure src="./images/japanese-keyboard-arch/gnome-settings-keyboard.png" alt="Capture d'écran des paramètres du clavier sous GNOME." position="center" caption="Paramètres du clavier sous GNOME." captionPosition="center">}}

Ensutie, cliquer sur "Ajouter une nouvelle méthode d'entrée" et sélectionner "Japonais".

{{< figure src="/images/japanese-keyboard-arch/gnome-settings-add-input-source.png" alt="Capture d'écran des paramètres du clavier sous GNOME - Choix de la méthode d'entrée." position="center" caption="Choix de la méthode d'entrée sous GNOME." captionPosition="center">}}

Enfin, *scroller* jusqu'à voir apparaitre "Japanese (Mozc:あ)". Cette version permet de directement passer sur une entrée en *kana*.

{{< figure src="/images/japanese-keyboard-arch/gnome-settings-select-input-source.png" alt="Capture d'écran des paramètres du clavier sous GNOME - Ajout du clavier hiragana." position="center" caption="Sélection du clavier Japanese (Mozc:あ)." captionPosition="center">}}

Pour changer de méthode d'entrée, le raccourci `<super> + <espace>` peut être employé. Enfin, lors de l'écriture, des *hiragana* s'affichent ainsi qu'une liste de mot. 

{{< figure src="/images/japanese-keyboard-arch/example.png" alt="Exemple d'utilisation du clavier japonais." position="center" caption="Exemple d'utilisation du clavier japonais." captionPosition="center">}}

Cette liste peut être naviguée à l'aide de la touche `<espace>`, et une entrée peut être sélectionnée en confirmant avec `<enter>`.