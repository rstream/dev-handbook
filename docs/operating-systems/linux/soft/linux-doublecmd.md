# Double Commander for Linux

[← back](../index.md)

`Double Commander` is a two-panel file manager for Linux, conceptually similar to `Total Commander`.

## Installation

### openSUSE

#### OPI

Use on openSUSE 16.0+
```sh
opi doublecmd
```

#### Manually

Use on openSUSE 15.6-
```sh
# add the repository
zypper addrepo https://download.opensuse.org/repositories/home:Alexx2000/openSUSE_Leap_15.5/home:Alexx2000.repo
# refresh the repository
zypper refresh
# install the package
zypper install doublecmd-qt6
```

## Configuration

### Configuration file

Configuration file is located at `~/.config/doublecmd/doublecmd.xml`.

To restore my configuration, use this asset:
[doublecmd.xml](assets/doublecmd/doublecmd.xml).


### Color theme

Color theme is located at `~/.config/doublecmd/colors.json`.

To restore my color theme, use this asset:
[colors.json](assets/doublecmd/colors.json).

### Enable natural sorting (file panels):

Navigate to: `Configuration > Options > File View`  
Sort Method = `Natural sorting: special characters sort`  
Sort directories = `sort by name and show first`

### Space move selection down

Edit `~/.config/doublecmd/doublecmd.xml` and add this line:
```
<SpaceMovesDown>True</SpaceMovesDown>
```
to the `<Miscellaneous>` section.

### Rename files: don’t touch extension

Navigate to: `Configuration > Options > File Operations`  
[x] select file name without extension when renaming

## Run as root

### Start Double Commander

If you need to start it as `root`, use:

```sh
kdesu doublecmd
```

> Note: when started as `root`, `Double Commander` uses root's own config directory, not your normal user profile

## Copy settings from your user to root

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

If the root config already exists, and you want to replace it with your user config:

```sh
sudo rm -rf /root/.config/doublecmd
sudo cp -a ~/.config/doublecmd /root/.config/
```

After that, when `Double Commander` is started as `root`, it will use the copied layout, tabs, hotkeys, and other settings.
