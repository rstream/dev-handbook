# Applications: icon files

[← back](../index.md)

Application icons in Linux desktop environments (`KDE Plasma`, `GNOME`, `Xfce`, etc.) are usually resolved through the icon theme system. In most cases the `.desktop` file does not point to a full icon path. Instead it contains an icon name, and the desktop environment looks that name up in the current icon theme and its fallbacks.

## How `Icon=` works in a `.desktop` file

Example:

```ini
Icon=sublime-text
```

This usually means:

* the icon name is `sublime-text`
* the desktop environment will try to find an icon file with that basename
* you normally do not put the extension in the `.desktop` file

So this line is typically matched against files like:

```text
sublime-text.png
sublime-text.svg
sublime-text.xpm
```

If `Icon=` contains an absolute path, the theme lookup is bypassed:

```ini
Icon=/opt/sublime_text/Icon/256x256/sublime-text.png
```

## Main icon locations

### User-level icons

Common user-level locations:

```text
~/.local/share/icons
~/.icons
```

Notes:

* `~/.local/share/icons` is the practical modern location for user-installed icons
* `~/.icons` is legacy, but many implementations still check it for compatibility

### System-level icons

Common system-level locations:

```text
/usr/share/icons
/usr/local/share/icons
/usr/share/pixmaps
```

Notes:

* `/usr/share/icons` is the standard system icon tree used by installed themes (main place)
* `/usr/local/share/icons` is a typical place for locally installed system-wide icons
* `/usr/share/pixmaps` is usually used as a fallback location for non-themed icons

## Theme structure

An icon theme is stored as a directory with an `index.theme` file and subdirectories for sizes and contexts.

Example:

```text
/usr/share/icons/breeze/index.theme
/usr/share/icons/breeze/16x16/apps/
/usr/share/icons/breeze/32x32/apps/
/usr/share/icons/breeze/48x48/apps/
/usr/share/icons/breeze/64x64/apps/
/usr/share/icons/breeze/scalable/apps/
```

Typical contexts:

* `apps` - application icons
* `mimetypes` - file type icons
* `places` - folders, home, mounted disks, etc.
* `actions` - toolbar/action icons

## `hicolor` theme

`hicolor` is the common fallback theme. Applications should install their icons there at minimum, so the desktop can still find an icon even if the currently selected theme does not provide one.

Typical application icon paths:

```text
/usr/share/icons/hicolor/48x48/apps/sublime-text.png
/usr/share/icons/hicolor/scalable/apps/sublime-text.svg
```

For a user-only application the same structure is usually used under:

```text
~/.local/share/icons/hicolor/48x48/apps/
~/.local/share/icons/hicolor/scalable/apps/
```

## How icon lookup typically works

When a desktop file contains:

```ini
Icon=sublime-text
```

the lookup is typically:

1. Search in the current icon theme (e.g. `breeze`)
2. If the current theme inherits from other themes, search in those inherited themes
3. If still not found, search in `hicolor`
4. If still not found, try fallback non-themed locations such as `/usr/share/pixmaps`

> Note: some applications (like Double Commander), do not search in `pixmaps` folder. That why DC does not show icon for VS Code.

Inside a theme, the lookup is not just "find any file with this name". The implementation also tries to choose the best matching size.

In simplified form:

1. Look for an exact size match in the current theme
2. If there is no exact match, look for the closest matching size in the same theme
3. Only after that move to inherited themes and finally to `hicolor`

This means a theme-provided icon generally wins over a fallback icon, even if the fallback has a size that looks slightly better.

## File extensions

Common supported icon formats:

* `.png`
* `.svg`
* `.xpm`

In the freedesktop icon theme lookup algorithm, the search order is typically:

1. `.png`
2. `.svg`
3. `.xpm`

In practice:

* `PNG` is the normal bitmap format
* `SVG` is useful for `scalable/` icons
* `XPM` exists mainly for compatibility with older setups

## Practical example

If you have:

```ini
[Desktop Entry]
Name=Sublime Text
Exec=/opt/sublime_text/sublime_text %F
Icon=sublime-text
Type=Application
```

then the desktop environment will try to resolve `sublime-text` through the current icon theme lookup rules.

For example, it may end up using one of these files:

```text
~/.local/share/icons/hicolor/48x48/apps/sublime-text.png
/usr/local/share/icons/hicolor/48x48/apps/sublime-text.png
/usr/share/icons/Papirus/48x48/apps/sublime-text.svg
/usr/share/icons/hicolor/scalable/apps/sublime-text.svg
/usr/share/pixmaps/sublime-text.png
```

Which one is actually used depends on:

* the current theme
* theme inheritance
* available sizes
* which of the searched files exists first in the lookup order

## Recommended install pattern

For a normal application launcher:

* put `Icon=my-app` in the `.desktop` file
* install the icon into the icon theme hierarchy
* at minimum provide an icon in `hicolor`

Common minimum setup:

```text
/usr/share/applications/my-app.desktop
/usr/share/icons/hicolor/48x48/apps/my-app.png
```

Better setup:

```text
/usr/share/applications/my-app.desktop
/usr/share/icons/hicolor/48x48/apps/my-app.png
/usr/share/icons/hicolor/scalable/apps/my-app.svg
```

## Practical note

If the `.desktop` file says:

```ini
Icon=sublime-text
```

then the filename should usually be based on the same icon name:

```text
sublime-text.png
sublime-text.svg
```

The name in `Icon=` is the basename the system searches for. The extension and concrete path are resolved by the icon theme lookup process.
