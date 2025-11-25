# Kate setup for C++

[← back](index.md)

Set up Kate for C++ development.  

## 1. Install compilers and Qt library

### GCC

GCC is usually a part of Linux, but the version may be outdated. Install the new version if you need it:
> [Install GCC](../../operating-systems/linux/linux-cpp.md)  

### Clang

Clang is required to make Kate understand C++ (even if you are using GCC)

> [Install clang](../../operating%20systems/linux/linux-cpp.md#clang)

### Qt

For cross-platform GUI development install Qt package

> [Install Qt](../../operating%20systems/linux/linux-qt.md)

## 2. Enable build plugin

Navigate to `Setting > Configure Kate > Plugins`  
Enable **Build Plugin**.  
After this `Build` menu will appear.

## 3. Create a Build Target

* In the **Target Settings** (at the bottom, below your code), create a new **Set of Targets** and add a new **Target** (give it any name), like this:
`g++ -g -std=c++17 "%f" -o "bin/%n" && "bin/%n"`
* then choose it (make highlighted)
* then select from the main menu `Build > Build Selected Target` (or `Build > Build and Run Selected Target` - these commands would actually do the same since we put `&& "bin/%n"` at the end of the build command)

> result: you source code would be compiled and executed

notes regarding the example above:
* **gcc (g++)** is used, so make sure it is installed (in proper version)
* folder `bin` should be created first (or compilation will fail)
* this setting would be global (not per-project)

## 4. Create a keyboard shortcut

To make a shorcut for `Build Selected Target` navigate to `Settings > Configure keyboard shortcuts` and find `Build and Run Selected Target`  
If you want to assign `F5` (as in VS Code) - be aware this shortcut would be removed from **reload** action.

## 5. Kate project settings

### General example

Setting up Kate project allows to define custom project level build/run tasks.  
Create a `.kateproject` file with the following content:
```json
{
  "name": "Kate project 3",
  "files": ["*.cpp"],
  "build": {
    "directory": ".",
    "targets": [
      {
        "name": "Build or run",
        "build_cmd": "g++ -g -std=c++17 \"%f\" -o \"bin/%n\"",
        "run_cmd": "./bin/kate3"
      },
      {
        "name": "Build and run",
        "build_cmd": "g++ -g -std=c++17 \"%f\" -o \"bin/%n\" && \"bin/%n\""
      }
    ]
  }
}
```
Notes:
* Have 2 targets (would be displayed at the bottom in the `Target Settings` tab)
* First target - with separate Build and Run tasks (⚠️ caveat: separate run tasks do not support %n, have to put bin file name)
* Second target - mixed one, where Build task also contains app launch; looks a bit weird, but helpful for learning (with simple projects, where you have multiple separate C++ files in a single dir)

### Example for Qt

When project requires additional headers (to include) and libraries (to link) - **like Qt** - they should also be put into the build task:

```json
{
  "name": "Kate project 3",
  "files": ["*.cpp"],
  "build": {
    "directory": ".",
    "targets": [
      {
        "name": "Build and run",
        "build_cmd": "g++ -g -std=c++20 \"%f\" -o \"bin/%n\" -I/usr/include/qt6 -I/usr/include/qt6/QtWidgets -I/usr/include/qt6/QtGui -I/usr/include/qt6/QtCore -lQt6Widgets -lQt6Gui -lQt6Core && \"bin/%n\""
      }
    ]
  }
}
```

## 6. Set up LSP (clang) for external libs

Two ways to make IntelliSense work with external libraries.

### 1) .clangd

Create a `.clangd` file with the content like this, and put to the project dir:
```
CompileFlags:
  CompilationDatabase: .
  Add: [
    "-std=c++17",
    "-I/usr/include/qt6",
    "-I/usr/include/qt6/QtWidgets",
    "-I/usr/include/qt6/QtGui",
    "-I/usr/include/qt6/QtCore"
  ]

Diagnostics:
  UnusedIncludes: Strict
```

> Notes:
* important to set C++ version 17 or higher

### 2) compile_commands.json
Create a `compile_commands.json` file with the content like this, and put to the project dir:

```json
[
	{
		"directory": "/data/DevU/C/16 Kate/3 kate-qt1",
		"command": "g++ -g -std=c++17 -I/usr/include/qt6 -I/usr/include/qt6/QtWidgets -I/usr/include/qt6/QtGui -I/usr/include/qt6/QtCore -o bin/kate-c-1 kate-c-1.cpp -lQt6Widgets -lQt6Gui -lQt6Core",
		"file": "./*.cpp"
	}
]

```

> Notes:
* have to specify absolute path to the project folder
* according to manuals "file" should point to a single file, but masks like "./\*" or "./\*.cpp" still work fine

There's a way to auto-generate `compile_commands.json` by script:

```sh
#!/bin/bash

SRC="kate-c-1.cpp"
OUT="bin/kate-c-1"
CXX="g++"
CXXFLAGS="-g -std=c++17"
INCLUDES="-I/usr/include/qt6 -I/usr/include/qt6/QtWidgets -I/usr/include/qt6/QtGui -I/usr/include/qt6/QtCore"
LIBS="-lQt6Widgets -lQt6Gui -lQt6Core"

mkdir -p bin

echo "[" > compile_commands.json
echo "{" >> compile_commands.json
echo "\"directory\": \"$(pwd)\"," >> compile_commands.json
echo "\"command\": \"$CXX $CXXFLAGS $INCLUDES -o $OUT $SRC $LIBS\"," >> compile_commands.json
echo "\"file\": \"$(pwd)/$SRC\"" >> compile_commands.json
echo "}" >> compile_commands.json
echo "]" >> compile_commands.json
```