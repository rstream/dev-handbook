# Qt for Linux

[← back](index.md)

For cross-platform GUI development install Qt package (in this example we install `Qt6`)

```sh
sudo zypper install libQt6Core6 libQt6Gui6 libQt6Widgets6 qt6-base-devel qt6-widgets-devel qt6-tools qt6-tools-devel qt6-tools-designer
```

This would install:

1. Qt runtime libs:

* libQt6Core6 — Qt Core (strings, files, timers, containers).
* libQt6Gui6 — graphics, fonts, images.
* libQt6Widgets6 — classic widgets (buttons, layouts, etc).

2. Dev-packages (headers and deployment tools):
* qt6-base-devel — headers for QtCore/Gui/Network and moc/uic/rcc.
* qt6-widgets-devel — headers for QtWidgets.

3. Qt Tools:
* qt6-tools — Qt Linguist, lrelease, qdoc, helpers.

4. Dev-packages for Qt Tools:
* qt6-tools-devel — headers for tools

5. Qt Designer:
* qt6-tools-designer — GUI-editor for interfaces (.ui)