# Basic setup

[← back](index.md)

## KDE desktops

KDE has 2 “graphics servers” (desktop rendering engines):

* Wayland (new, high performance, very smooth on high-Hz displays, supports separate scaling for dual-monitor systems)
* X11 (old, more compatible with old software, less performance, high-Hz displays will look like 60 Hz)
X11 is set by default.

You can switch to Wayland on the login screen (at the bottom, in the desktop selection list).

## KDE Plasma window decoration

Make minimize/maximize/close buttons large and square:  
`Start > System > System Settings > Colors & Themes > Window Decorations`

Choose "Plastik".

## Codecs

New recommended way to install codecs - using OPI (OBS Package Installer).

```bash
sudo zypper install opi
opi codecs
```

This command will add Packman repository and install codecs from there.

## Terminal font

To set up font size for Konsole:

* Go to `Settings > Configure Konsole...`
* In the `Profiles` section create a new profile
* Mark it as default
* Edit the new profile
* On the `Appearance` section set the font size
