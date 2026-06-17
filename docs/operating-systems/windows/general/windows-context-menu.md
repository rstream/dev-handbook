# Windows context menu via Registry — quick reference

[← back](../index.md)

## 1. Scope: all users vs current user

### All users

Use:

```reg
HKEY_CLASSES_ROOT
```

Examples:

```reg
HKEY_CLASSES_ROOT\Directory\shell
HKEY_CLASSES_ROOT\*\shell
HKEY_CLASSES_ROOT\Drive\shell
```

Usually requires administrator rights.

`HKCR` is a merged view of:

```reg
HKEY_LOCAL_MACHINE\Software\Classes
HKEY_CURRENT_USER\Software\Classes
```

### Current user only

Use:

```reg
HKEY_CURRENT_USER\Software\Classes
```

Examples:

```reg
HKEY_CURRENT_USER\Software\Classes\Directory\shell
HKEY_CURRENT_USER\Software\Classes\*\shell
```

Usually does not require administrator rights.

## 2. Where to add menu items

### For folders

Right-click on a folder:

```reg
...\Directory\shell
```

Example:

```reg
HKCR\Directory\shell\MyMenuItem
HKCR\Directory\shell\MyMenuItem\command
```

### For folder background

Right-click on empty space inside a folder:

```reg
...\Directory\Background\shell
```

Example:

```reg
HKCR\Directory\Background\shell\MyMenuItem
HKCR\Directory\Background\shell\MyMenuItem\command
```

### For drives

Right-click on `C:`, `D:`, etc.:

```reg
...\Drive\shell
```

Example:

```reg
HKCR\Drive\shell\MyMenuItem
HKCR\Drive\shell\MyMenuItem\command
```

### For all files

Right-click on any file:

```reg
...\*\shell
```

Example:

```reg
HKCR\*\shell\MyMenuItem
HKCR\*\shell\MyMenuItem\command
```

### For specific file types

For example, `.txt`.

First check the file type:

```cmd
assoc .txt
```

Example result:

```cmd
.txt=txtfile
```

Then add the menu item under:

```reg
HKCR\txtfile\shell
```

Example:

```reg
HKCR\txtfile\shell\MyMenuItem
HKCR\txtfile\shell\MyMenuItem\command
```

Directly using the extension is possible:

```reg
HKCR\.txt\shell
```

but using the real file type, like `txtfile`, is usually cleaner.

## 3. Basic menu item structure

A simple item needs two keys:

```reg
...\shell\MyMenuItem
...\shell\MyMenuItem\command
```

In `MyMenuItem`, set display options.

In `command`, set the default value to the command line.

Example command value:

```reg
"C:\Path\To\app.exe" "%1"
```

## 4. Menu item name

You can set the visible name in two common ways.

### Default value

```reg
@="Open with My App"
```

### `MUIVerb`

```reg
"MUIVerb"="Open with My App"
```

`MUIVerb` is the visible menu label.

If neither is set, Windows usually shows the key name:

```reg
...\shell\VSCode
```

Menu text:

```text
VSCode
```

## 5. Icon

Use the `Icon` string value in the menu item key.

Examples:

```reg
"Icon"="C:\Path\To\app.exe"
```

```reg
"Icon"="C:\Icons\myicon.ico"
```

```reg
"Icon"="shell32.dll,3"
```

## 6. Parameters

Most useful placeholders:

| Placeholder | Meaning                                              |
| ----------- | ---------------------------------------------------- |
| `%1`        | selected file or folder                              |
| `%V`        | current folder when right-clicking folder background |
| `%L`        | long file/path name                                  |
| `%*`        | all arguments                                        |

Typical usage:

### Folder or file item

```reg
"C:\Path\To\app.exe" "%1"
```

### Folder background item

```reg
"C:\Path\To\app.exe" "%V"
```

Always quote placeholders, because paths may contain spaces.

Good:

```reg
"C:\Program Files\App\app.exe" "%1"
```

Bad:

```reg
C:\Program Files\App\app.exe %1
```

## 7. Submenus

A submenu has this structure:

```reg
...\shell\Development
...\shell\Development\shell\SublimeText
...\shell\Development\shell\SublimeText\command
...\shell\Development\shell\VSCode
...\shell\Development\shell\VSCode\command
```

The parent item usually has:

```reg
"MUIVerb"="Development"
"SubCommands"=""
```

The child items are normal menu items with their own `command` keys.

## 8. Position

You can hint the menu position with:

```reg
"Position"="Top"
```

or:

```reg
"Position"="Bottom"
```

## 9. Removing an item

Delete the whole key:

```reg
...\shell\MyMenuItem
```

For example:

```reg
HKCR\Directory\shell\VSCode
```

or for current user:

```reg
HKCU\Software\Classes\Directory\shell\VSCode
```

## 10. Quick map

| Target             | Registry path                            |
| ------------------ | ---------------------------------------- |
| Folders            | `HKCR\Directory\shell`                   |
| Folder background  | `HKCR\Directory\Background\shell`        |
| Drives             | `HKCR\Drive\shell`                       |
| All files          | `HKCR\*\shell`                           |
| Specific file type | `HKCR\<filetype>\shell`                  |
| Current user only  | `HKCU\Software\Classes\...`              |
| All users          | `HKCR\...` / `HKLM\Software\Classes\...` |

## 11. Common values

| Value             | Purpose                      |
| ----------------- | ---------------------------- |
| default value `@` | visible menu label           |
| `MUIVerb`         | visible menu label           |
| `Icon`            | menu icon                    |
| `command` key     | command to execute           |
| `%1`              | selected item path           |
| `%V`              | current folder path          |
| `SubCommands`     | enables submenu-style parent |
| `Position`        | `Top` / `Bottom`             |
