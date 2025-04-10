+++
title = "Configuring the Japanese keyboard on Arch Linux"
date = "2025-04-10T19:29:48+02:00"
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

Japanese fonts must be installed. Be aware that some characters are slightly different in Chinese. I recommend installing Noto.

```bash
sudo pacman -S --needed noto-fonts noto-fonts-cjk
```

More fonts can be found on the [wiki](https://wiki.archlinux.org/title/Localization/Japanese) and on Tatsumoto Ren's [blog](https://tatsumoto-ren.github.io/blog/resources.html#fonts).

### Japanese locale

Locales are used by locale-aware programs and libraries for rendering text, displaying regional monetary values, time and date formats and other locale-specific standards. If this has not been generated, some font rendering issues might appear[^1].

[^1]: Archwiki, *[Localization/Japanese](https://wiki.archlinux.org/title/Localization/Japanese)*

To add a Japanese locale to your system, modify the `/etc/locale.gen` file and uncomment the `ja_JP.UTF8 UTF8` line by removing the `#` at the beginning of the line. The file should look something like this:

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

Once modified, save it and run `locale-gen` to generate the locale(s). Both actions require root privileges (`sudo`).

You can verify that the Japanese locale has been properly enabled if it is listed in the output of the `locale -a` command which lists all enabled locales. For reference, I get the following output:

```txt
[akari@nyarch ~]$ locale -a
C
C.utf8
en_US.utf8
fr_CH.utf8
ja_JP.utf8
POSIX
```

## Installing and configuring the keyboard

A Japanese keyboard requires two components to work correctly:

- An input method framework (IMF) to let the user switch between IMEs.
- An input method editor (IME) to convert Latin characters to Japanese kanas and kanjis.

On GTK-based environments (GNOME, Mate, ...), the commonly found IMF is called IBus, while on  Qt-based environments such as KDE Plasma, Fctix5 is more common. Both work with all IMEs.

A variety of IMEs exist (see the [wiki](https://wiki.archlinux.org/title/Localization/Japanese#Input_Method_Editor_%28IME%29)), but the most used one is mozc, which is an open source project based on the Google Japanese Input. All packages can be found in the official repositories of Arch Linux, with the exception of `ibus-mozc` which sits in the AUR.

```bash
# On GTK-based desktops
sudo pacman -S ibus
paru -S ibus-mozc
```

```bash
# On Qt-based desktops
sudo pacman -S fcitx5-im fcitx5-mozc
```

Then, three or four environment variables must be set, depending on the IMF, which  done by adding the following lines to the `~/.config/environment.d/envvars.conf` file.

```cfg
# On GTK-based environments
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
MOZC_IBUS_CANDIDATE_WINDOW=ibus
```

```cfg
# On Qt-based environments
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

Note that the environment variables for fcitx do not include a 5.

Finally, you can add the keyboard layout to your session. On my system, which is based around GNOME, the input source can be added through the settings *Keyboard* > *Input Sources* > *Add Input Source* > *Japanese*.

