+++
title = "Configuring the Japanese keyboard on Arch Linux"
date = "2025-04-10T19:29:48+02:00"
lastmod = "2025-05-01T10:01:48+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["linux", "japanese"]
keywords = ["", ""]
description = "In this short post, I'll explain how to configure a Japanese keyboard on Arch Linux."
showFullContent = false
readingTime = true
hideComments = false
+++

## Prerequistes

### Fonts

By default, the system lacks Japanese fonts. Therefore, installing at least one font is necessary to properly display *kana* and *kanji* characters.

I recommend using the *Noto* font, as it is fairly complete and distributed under a free (as in freedom) license.

```bash
sudo pacman -S --needed noto-fonts noto-fonts-cjk
```

The first package will install the "base" font containing letters (Latin, Cyrillic, ...), while the second package focuses on logographs (*kanji*, *hanzi*, *hanja*, ...).

More fonts can be found on the [Arch Wiki](https://wiki.archlinux.org/title/Localization/Japanese). A selection of fonts can also be found on Tatsumoto Ren's [blog](https://tatsumoto-ren.github.io/blog/resources.html#fonts).

> Be careful as some characters are written differently in Chinese and Japanese! For instance, the `直` character lacks a vertical stroke on the left in Chinese[^1].

[^1]: Wiktionary, *[直 - Alternative forms](https://en.wiktionary.org/wiki/%E7%9B%B4#Alternative_forms)* 

### Japanese locale

Locales are used by the system to render fonts and format regional-specific elements (money, dates, time, ...). If a locale is missing, some font rendering issues might occur[^2].

[^2]: Archwiki, *[Localization/Japanese](https://wiki.archlinux.org/title/Localization/Japanese)*

A locale can be added to the system via the `/etc/locale.gen` file, which is as a reference by the system when generating locales. To add the Japanese locale, uncomment the `ja_JP.UTF8 UTF8` by removing the leading `#`. Do not disable any already enabled locales.

```bash
sudo vim /etc/locale.gen
```

The file content should look something like this:

```cfg
# File: /etc/locale.gen
# ...
#iu_CA UTF-8  
#ja_JP.EUC-JP EUC-JP  
ja_JP.UTF-8 UTF-8  
#ka_GE.UTF-8 UTF-8  
#ka_GE GEORGIAN-PS
# ...
```

Once the line has been uncommented, save the file and run the following command to generate locales.

```bash
sudo locale-gen
```

You can then check if the Japanese locale has been properly enabled by listing all enabled locales using the `locale -a` command. The locale has been properly generated if `ja_JP.utf8` is present in the list.

For reference, here is the output I get on my system:

```txt
[akari@nyarch ~]$ locale -a
C
C.utf8
en_US.utf8
fr_CH.utf8
ja_JP.utf8
POSIX
```

## Japanese keyboard

### Components

A Japanese keyboard requires two compenents to work correctly:

- An *input method editor* (IME), which converts Latin script into *kana* and *kanji*.
- An *input method framework* (IMF) to let the user switch between IMEs.

There are two IMFs: [IBus](https://wiki.archlinux.org/title/IBus) and [Fctix5](https://wiki.archlinux.org/title/Fcitx5). The former is most commonly used on GTK-based environments such as GNOME or Mate, while the latter is preferred on Qt-based environments like KDE Plasma or LXQt. Both framework are compatible with all IMEs.

The most commonly recommended IME seems[^3] to be [Mozc](https://github.com/google/mozc), which is the one I personnally use. It is an open-source project based on *Google Japanese Input*.

[^3]: Alternatives can be found on the wiki: Archwiki, *[IME](https://wiki.archlinux.org/title/Localization/Japanese#Input_Method_Editor_%28IME%29)*

### GTK

On GTK-based environments, the `ibus` and `ibus-mozc` packages must be installed. Note that the former is available in the official *Arch Linux* repositories, while the latter must be installed from the AUR.

```bash
sudo pacman -S ibus
paru -S ibus-mozc
```

Then, four environment variables must be added. This can be done by adding the following lines to the `~/.config/environment.d/envvars.conf` file (can be created if it does not exist).

```cfg
# File $HOME/.config/environment.d/envvars.conf
# /!\ Works only on Wayland sessions /!\
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
MOZC_IBUS_CANDIDATE_WINDOW=ibus
```

### Qt

On Qt-based environments, the packages `fcitx5-im` and `fcitx5-mozc` must be installed. Both can be found in the official *Arch Linux* repositories.

```bash
sudo pacman -S fcitx5-im fcitx5-mozc
```

With Fcitx5, only three environment variables are required. These can also be placed in the `~/.config/environment.d/envvars.conf` file, which can be created if it does not exists.

```cfg
# File $HOME/.config/environment.d/envvars.conf
# /!\ Works only on Wayland sessions /!\
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

Note that the environment variables for Fcitx do not include "5" in their values!

### Usage

Once everything has been installed an configured, the Japanese keyboard can be used.

Adding a new keyboard differs depending on the desktop environment or window manager / compositor. On GNOME-based systems, an input method can be added through the *Keyboard* section of the *Settings* application. 

{{< figure src="/images/posts/japanese-keyboard-arch/gnome-settings-keyboard.png" alt="Screenshot of the keyboard section of the GNOME settings." position="center" caption="Keyboard settings on GNOME." captionPosition="center">}}

Then, click on *Add input source* and choose *Japanese*.

{{< figure src="/images/posts/japanese-keyboard-arch/gnome-settings-add-input-source.png" alt="Screenshot of the keyboard section of the GNOME settings - Input source choice." position="center" caption="Choosing the Japanese input source." captionPosition="center">}}

Finally, scroll to "Japanese (Mozc:あ)". This variants defaults the keyboard to *kana* input instead of *roumaji*.

{{< figure src="/images/posts/japanese-keyboard-arch/gnome-settings-select-input-source.png" alt="Screenshot of the keyboard section of the GNOME settings - Adding hiragana keyboard." position="center" caption="Selecting the Japanese (Mozc:あ) keyboard." captionPosition="center">}}

To change input method, the keyboard shortcut `<super> + <space>` can be used. When text is typed, a list of word suggestions appear.

{{< figure src="/images/posts/japanese-keyboard-arch/example.png" alt="Japanese keyboard usage example." position="center" caption="The words list." captionPosition="center">}}

One can navigate through that list using the `<space>` key. An entry can be selected using `<enter>`.