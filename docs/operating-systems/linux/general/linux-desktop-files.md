# Applications: .desktop files

[← back](../index.md)

`.desktop` files are application launcher descriptors used by Linux desktop environments (`KDE Plasma`, `GNOME`, `Xfce`, etc.). They describe how an application should appear in menus/search, which command should be executed, which icon should be shown, whether the app runs in terminal, which categories it belongs to, and which MIME types it can handle.

## Main locations

### System level

Desktop files available for all users are usually stored in:

```text
/usr/share/applications
/usr/local/share/applications
```

Typical usage:

* `/usr/share/applications` - entries installed by the package manager
* `/usr/local/share/applications` - locally installed custom entries for all users

### Current user level

Desktop files available only for the current user are usually stored in:

```text
~/.local/share/applications
```

This is the standard place for:

* custom launchers created manually
* user-specific overrides of system launchers
* entries for applications installed only into the user profile

## Priority and override behavior

If a desktop file with the same name exists both in the system location and in the user location, the user version takes precedence.

Example:

```text
/usr/share/applications/code.desktop
~/.local/share/applications/code.desktop
```

In this case the desktop environment will use the file from `~/.local/share/applications`.

## What `.desktop` files are used for

Desktop environments use them to:

* show applications in the app menu
* make applications searchable in launchers
* define the command used to start an application
* attach an icon and display name
* decide whether the app is graphical or terminal-based
* group apps into menu categories
* register file type handlers via `MimeType`

## Basic structure

A `.desktop` file is a text file similar to an INI file. The main section is usually `[Desktop Entry]`.

Example:

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=My App
Comment=Start My App
Exec=/opt/my-app/bin/my-app %U
Icon=my-app
Terminal=false
Categories=Development;IDE;
MimeType=text/plain;
StartupNotify=true
```

## Most common fields

### Required or commonly expected

* `Type` - usually `Application`
* `Name` - application name shown in menus
* `Exec` - command used to start the application

### Frequently used optional fields

* `Comment` - short description
* `Icon` - icon name or absolute path to an icon file
* `Terminal` - `true` if the app should run inside a terminal
* `Categories` - menu grouping, for example `Utility;Development;`
* `MimeType` - file types the app can open
* `StartupNotify` - whether startup notification should be shown
* `Path` - working directory for the application
* `NoDisplay` - hide from menus, but keep entry usable internally
* `Hidden` - disable the entry

## Notes about `Exec`

The `Exec` field can contain field codes used by the desktop environment:

* `%f` - one file
* `%F` - multiple files
* `%u` - one URL
* `%U` - multiple URLs
* `%i` - icon
* `%c` - translated application name

Example:

```ini
Exec=/usr/bin/vlc %U
```

## MIME types and `Open With`

To make an application appear in `Open With` for some file type, the desktop entry usually needs:

* a `MimeType=` field with one or more supported MIME types
* a suitable `Exec=` command that can accept file paths or URLs

Example for text files:

```ini
MimeType=text/plain;
Exec=/opt/my-app/bin/my-app %F
```

### Basic examples

For plain text files:

```ini
MimeType=text/plain;
```

For directories (folders):

```ini
MimeType=inode/directory;
```

For several types at once:

```ini
MimeType=text/plain;inode/directory;
```

This means the application can be offered in `Open With` both for text files and for folders.

### Which `Exec` placeholder to use

Usually:

* `%f` / `%F` - when your app expects local file paths
* `%u` / `%U` - when your app can accept URLs and desktop items in addition to regular paths

For most editors and GUI tools working with normal files, `%F` is the usual choice.

For applications that can open folders, the command should also accept a directory path, for example:

```ini
Exec=/opt/my-app/bin/my-app %F
MimeType=inode/directory;
```

### Important limitation

Adding `MimeType` only declares that the application supports a type. Whether it appears in a specific file manager's `Open With` menu can still depend on the desktop environment, file manager behavior, and user associations.

## Default app associations

The default application for a MIME type is usually stored in `mimeapps.list`.

Common user-level location:

```text
~/.config/mimeapps.list
```

Typical format:

```ini
[Default Applications]
text/plain=my-app.desktop
inode/directory=my-app.desktop
```

This does not replace the need for `MimeType=` in the `.desktop` file. Usually you need both:

* `MimeType=` in the application desktop entry
* an association in `mimeapps.list` if you want it to become the default app

## Minimal example

Example of a launcher that can open text files and folders:

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=My App
Exec=/opt/my-app/bin/my-app %F
Icon=my-app
Terminal=false
MimeType=text/plain;inode/directory;
Categories=Utility;Development;
```

## Useful MIME commands

Check MIME type of a file:

```sh
file --mime-type my-file.txt
```

Check current default app for a MIME type:

```sh
xdg-mime query default text/plain
xdg-mime query default inode/directory
```

Set default app for a MIME type:

```sh
xdg-mime default my-app.desktop text/plain
xdg-mime default my-app.desktop inode/directory
```

## Useful commands

List system desktop files:

```sh
ls /usr/share/applications
```

List user desktop files:

```sh
ls ~/.local/share/applications
```

Create a user-level desktop file:

```sh
mkdir -p ~/.local/share/applications
```

## Practical note

When you want to customize a launcher without touching package-managed files, copy the system entry into `~/.local/share/applications` and edit it there. This avoids losing changes during package updates.

## Example

### Sublime text

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=/opt/sublime_text/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=sublime-text
Categories=TextEditor;Development;
StartupNotify=true
Actions=new-window;new-file;

[Desktop Action new-window]
Name=New Window
Exec=/opt/sublime_text/sublime_text --launch-or-new-window
OnlyShowIn=Unity;

[Desktop Action new-file]
Name=New File
Exec=/opt/sublime_text/sublime_text --command new_file
OnlyShowIn=Unity;
```
