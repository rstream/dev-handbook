# Compilation of the Qt application

[← back](../index.md)

To compile a Qt app you need to include Qt headers and link Qt libraries.

Include headers:
* /usr/include/qt6
* /usr/include/qt6/QtWidgets
* /usr/include/qt6/QtGui
* /usr/include/qt6/QtCore

Link libraries:
* Qt6Widgets
* Qt6Gui
* Qt6Core

Command line example:
```sh
g++ hello-world.cpp -g -o bin/hello-world -I/usr/include/qt6 -I/usr/include/qt6/QtWidgets -I/usr/include/qt6/QtGui -I/usr/include/qt6/QtCore -lQt6Widgets -lQt6Gui -lQt6Cor
```

