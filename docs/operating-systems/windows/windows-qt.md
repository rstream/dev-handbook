# Qt for Windows

[← back](index.md)

For cross-platform GUI development install Qt package (in this example we install `Qt6`).

## Install Qt with the official installer

Go to the Qt download page:

```text
https://www.qt.io/download-qt-installer-oss
```

Download and run the Windows online installer.

During installation select:

1. Qt runtime and development packages:

* Qt 6.x.x - the Qt version you want to use.
* MinGW kit - choose it if you want a ready-to-use GCC-based compiler.
* MSVC kit - choose it if you want to build with Microsoft Visual Studio compiler.

2. Development tools:

* Qt Creator - IDE for Qt projects.
* Qt Design Studio - optional visual editor for UI-heavy projects.
* Debugging Tools for Windows - useful for debugging MSVC builds.

3. Qt modules:

* Qt Core - strings, files, timers, containers.
* Qt Gui - graphics, fonts, images.
* Qt Widgets - classic widgets (buttons, layouts, etc).
* Qt Network - networking classes.

## Compiler notes

For beginners, choose the `MinGW` kit in the Qt installer. It installs Qt, Qt Creator and a compatible compiler in one place.

If you choose the `MSVC` kit, install Visual Studio Build Tools first and include:

* MSVC C++ build tools.
* Windows SDK.
* CMake tools for Windows.
