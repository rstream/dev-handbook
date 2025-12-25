# Compilation of the Qt application

[← back](../index.md)

## Compiling a C++ Qt app

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

## Setting up editors for Qt app compilation

To make Qt work with your editor you need to set up:
* build tasks (compilation)
* IntelliSense settings

### Kate

[KATE - compilation](../../../../editors/kate/kate-cpp.md#example-for-qt) - Kate project settings for Qt compilation  
[KATE - IntelliSense](../../../../editors/kate/kate-cpp.md#6-set-up-lsp-clang-for-external-libs) - Kate clang settings for Qt IntelliSense

### VS Code

[VS Code - compilation](../../../../editors/vscode/vscode-cpp.md#build-configuration-for-qt) - VS Code project settings for Qt compilation  
[VS Code - IntelliSense](../../../../editors/vscode/vscode-cpp.md#configuration-for-qt) - VS Code project settings for Qt IntelliSense
