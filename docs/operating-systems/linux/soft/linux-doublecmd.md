# Double Commander for Linux

[← back](../index.md)

`Double Commander` is a two-panel file manager for Linux, conceptually similar to `Total Commander`.

## Installation

### openSUSE

```sh
sudo zypper install doublecmd-qt6
```

`doublecmd-gtk` is the usual package for GTK-based desktops. Some distributions also provide a Qt build such as `doublecmd-qt`.

## Run as root

If you still need to start it as `root`, use:

```sh
kdesu doublecmd
```

> Note: when started as `root`, `Double Commander` uses root's own config directory, not your normal user profile

## Copy user settings to root

User settings are usually stored here:

```text
~/.config/doublecmd
```

For the `root` account, the config is typically:

```text
/root/.config/doublecmd
```

To copy your current user settings to the `root` profile:

```sh
sudo mkdir -p /root/.config
sudo cp -a ~/.config/doublecmd /root/.config/
```

If the root config already exists and you want to replace it with your user config:

```sh
sudo rm -rf /root/.config/doublecmd
sudo cp -a ~/.config/doublecmd /root/.config/
```

After that, when `Double Commander` is started as `root`, it will use the copied layout, tabs, hotkeys, and other settings.
