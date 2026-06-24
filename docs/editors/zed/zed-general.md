# General

[← back](index.md)

General setup for Zed.

## Move File Manager to the left side

* Right-click on the blue **project panel** icon at the bottom-right corner.  
* Select "Dock Left"

## Set custom color theme

* Open Extensions: `Ctrl + Shift + X`.  
* Install the theme you like, e.g. `Jetbrains Darcula theme`.  
* Select the new theme: `theme selector: toggle` in Command Palette.

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