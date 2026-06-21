# General

[← back](index.md)

General setup for Zed.

## Move File Manager to the left side

* Right-click on the blue **project panel** icon at the bottom-right corner.  
* Select "Dock Left"

## Set Tab size

Open settings `Alt + Ctrl + ,`, add a tab size key:
```json
{
  "tab_size": 4
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