# General

[← back](../index.md)

General setup for Zed.

## Move File Manager to the left side

* Right-click on the blue **project panel** icon at the bottom-right corner.  
* Select "Dock Left"

## Set custom color theme

### Select custom theme

* Open Extensions: `Ctrl + Shift + X`.  
* Install the theme you like, e.g. `Jetbrains Darcula theme`.  
* Select the new theme: `theme selector: toggle` in Command Palette.

### Customize theme

To customize an existing theme you can use Zed Theme Builder:  
https://zed.dev/theme-builder

Find any existing theme, like this:
```
~/.local/share/zed/extensions/installed/jetbrains-darcula-theme-by-bronya0/themes/jetbrains-darcula-theme-by-bronya0.json
```
Import it to the Theme Builder and customize it.  
Then export the diff (override) and put it to the Zed `setting.json`.

My diff for the `darcula-theme-by-bronya0` you can [view here](./rstream-darcula-theme-by-bronya0-override.json).

## Set Tab size

Open settings `Alt + Ctrl + ,`, add a tab size key:
```json
{
    "tab_size": 4
}
```

## Disable trailing comma

Open settings `Alt + Ctrl + ,`, add a prettier setting:
```json
{
    "prettier": {
        "trailingComma": "none"
    }
}
```


## Key bindings

To edit key bindings - go to menu `Zed > Open Key Map`.
or edit `keymap.json`:
```
C:\Users\<user-name>\AppData\Roaming\Zed\keymap.json
```

### Save all

To bind saving all files override the `workspace: save all` action.

To bind `Ctrl + S` (and unbind default key) create new binding via UI or add these lines to `keymap.json`:
```json
[
    {
        "context": "Workspace",
        "bindings": {
            "ctrl-s": "workspace::SaveAll"
        }
    },
    {
        "context": "Workspace",
        "unbind": {
            "ctrl-k s": "workspace::SaveAll"
        }
    }
]
```

## "Open folder with..."

To add Zed to the `Open folder with...` context menu of the file explorer:  
* edit its `.desktop` file: `~/.local/share/applications/dev.zed.Zed.desktop`
* add `inode/directory` to the `MimeType` (semicolon separated)

## Turn off font ligatures

To disable transformation of "->", "=>", "!=" into special symbols - change the editor font from ".ZedMono" to something different (like "Droid Sans Mono" - used in VS Code).

Go to `Settings > Appearance > UI Font` and in the `Buffer Font` section set `Font Family` to "Droid Sans Mono".

Or add to `settings.json`:
```json
{
  "buffer_font_family": "Droid Sans Mono"
}
```
