# Compilation of the Qt application

[← back](index.md)

## Summary

- [Compiling a C++ Qt app](#compiling-a-cpp-qt-app)
- [Header paths](#header-paths)
- [Libraries](#libraries)
- [Command line example](#command-line-example)
- [Notes](#notes)
- [Setting up editors for Qt app compilation](#setting-up-editors-for-qt-app-compilation)

## <a id="compiling-a-cpp-qt-app"></a>Compiling a C++ Qt app

To compile a Qt app you need to include Qt headers and link Qt libraries. For a simple Qt Widgets application, the usual modules are `QtWidgets`, `QtGui`, and `QtCore`.

## <a id="header-paths"></a>Header paths

* /usr/include/qt6
* /usr/include/qt6/QtWidgets
* /usr/include/qt6/QtGui
* /usr/include/qt6/QtCore

## <a id="libraries"></a>Libraries

* Qt6Widgets
* Qt6Gui
* Qt6Core

## <a id="command-line-example"></a>Command line example

```sh
g++ -g hello-world.cpp -I/usr/include/qt6 -I/usr/include/qt6/QtWidgets -I/usr/include/qt6/QtGui -I/usr/include/qt6/QtCore -lQt6Widgets -lQt6Gui -lQt6Core -o bin/hello-world
```

## <a id="notes"></a>Notes

* `QtWidgets` depends on `QtGui` and `QtCore`, but explicit libraries make the command easier to understand.
* Header and library paths can differ by distribution and installation method.
* For bigger projects, prefer CMake or qmake instead of maintaining long compiler commands manually.

## <a id="setting-up-editors-for-qt-app-compilation"></a>Setting up editors for Qt app compilation

To make Qt work with your editor you need to set up:
* build tasks (compilation)
* IntelliSense settings

### Kate

[KATE - compilation](../../../../editors/kate/kate-cpp.md#example-for-qt) - Kate project settings for Qt compilation  
[KATE - IntelliSense](../../../../editors/kate/kate-cpp.md#6-set-up-lsp-clang-for-external-libs) - Kate clang settings for Qt IntelliSense

### VS Code

[VS Code - compilation](../../../../editors/vscode/vscode-cpp.md#build-configuration-for-qt) - VS Code project settings for Qt compilation  
[VS Code - IntelliSense](../../../../editors/vscode/vscode-cpp.md#configuration-for-qt) - VS Code project settings for Qt IntelliSense
