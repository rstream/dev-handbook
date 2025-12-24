# VS Code setup for C++

[← back](index.md)

Set up VS Code for building and running C++ apps.

## 1. Install compilers

First of all - install C++ compilers:  
[Instruction for Linux](../../operating-systems/linux/linux-cpp.md)  
[Instruction for Windows](../../operating-systems/windows/windows-cpp.md)

## 2. Install extensions

### Install C/C++ Extension Pack

This extension connects VS Code with the compiler.  
Required for building `executable` files.

**Navigate:**  
> View > Extensions

or press `Ctrl+Shift+X`  

Search and install `C/C++ Extension Pack`

### Install **C/C++** extension (by Microsoft)

Required for **running and debugging** C++ code.

**Navigate:**  
> View > Extensions

or press `Ctrl+Shift+X`  

Search and install `C/C++`

### Install **CodeLLDB** extension

For using LLDB with VS Code as a debugger you need to install this exension.

**Navigate:**  
> View > Extensions

or press `Ctrl+Shift+X`  

Search and install `CodeLLDB`

## 3. Set up project settings

To set everything up you need 3 things:
1. UI configuration - for intellisense
2. Build task - for compilation
3. Run/debug task - for running and debugging

### 1) Add UI configuration

`Shift+Ctrl+P` (or `F1`) > `"C/C++: Edit configurations (UI)"`  
or  
Click `"Win32"` or `"Linux"` in the bottom-right corener > `Edit configurations (UI)`

**IntelliSense Configurations** page will appear  
the following file is created:
> ./.vscode/c_cpp_properties.json

it defines:
* includePath: path to `*.h` folders
* compilerPath: path to compiler for intelliSenseMode (not for build)
* cStandard / cppStandard: C/C++ standard
* intelliSenseMode: mode for intelliSenseMode
used for IntelliSense/autocomplete

example of `c_cpp_properties.json`:

#### Windows

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "C:\\Soft\\mingw64\\bin\\g++.exe",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

Notes:
* "Win32" is just a name (label) of the config, does not mean 32-bit app; you can rename it

#### Linux

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/include",
                "/usr/include/c++/14",
                "/usr/include/c++/14/x86_64-suse-linux"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/g++",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "linux-gcc-x64"
        }
    ],
    "version": 4
}
```

Notes:
* by default **includePath** contains only current project path; for correct autocomplete for standard C++ libs - also add their paths (included into the example above)
* path `/usr/include/c++/14/x86_64-suse-linux` would be different for the other versions of Linux
* by default the compiler is set to `gcc`; change it to `g++` if you are using C++ (not C)
* "compilerPath" is short (`/usr/bin/g++`) since we created a symlink for `/usr/bin/g++-14` (check [creating symlinks for GCC](../../operating-systems/linux/linux-cpp.md#create-symlinks))

### 2) Configure build task

#### Windows

Navigate to:
`Terminal → Configure Default Build Task...`  
or  
`Shift+Ctrl+P > Tasks: Configure Task`  

choose: `C/C++: g++.exe build active file`

example of **tasks.json**:

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++.exe build active file",
			"command": "C:\\Soft\\mingw64\\bin\\g++.exe",
			"args": [
				"-fdiagnostics-color=always",
				"-g",
				"-std=c++17",
				"-Wall",
				"-Werror",
				"-pedantic",
				"${file}",
				"-o",
				"${fileDirname}\\_build\\${fileBasenameNoExtension}.exe"
			],
			"options": {
				"cwd": "${fileDirname}"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"detail": "compiler: C:\\Soft\\mingw64\\bin\\g++.exe"
		}
	]
}
```

Notes:
* `${fileDirname}\\_build\\${fileBasenameNoExtension}.exe` - is a path to output (exe) file. You should set the same path in the Run/debug task ("program" key) to make sure debugger will find EXE file
* `-std=c++17` - clean C++ 17; if not set - some "specific" standard may be used, like `gnu++16`

#### Linux

Navigate to:
> Terminal → Configure Default Build Task...

choose `Create tasks.json file from template` > `Others`  
the create file is:
> ./.vscode/tasks.json

**Note:** dummy non-c++ task would be created - replace with the exaple below

a build task will be there, which defines:
* path to compiler
* command line parameters for compiler

example of `tasks.json`:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "C/C++: g++ build active file",
            "type": "shell",
            "command": "/usr/bin/g++",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "-std=c++17",
                "-Wall",
                "-Werror",
                "-pedantic",
                "${file}",
                "-o",
                "${fileDirname}/bin/${fileBasenameNoExtension}"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "detail": "Generated task by Debugger."
        }
    ]
}
```

### 3) Configure run/debug task

> Shift+Ctrl+P > C/C++: Add Debug Configuration > g++.exe build and debug active file

now `./.vscode/launch.json` is created!

it defines:
* `miDebuggerPath` - path to debugger (GDB or LLDB)
* `program` - path to your "exe"/"elf" file
* `preLaunchTask` - name of the build task (from "tasks.json") - to make sure "exe" is created before running/debugging it
* `stopAtEntry` - should stop on 1st line (as if there's a breakpoint there)
* `externalConsole` - program output to external console (new window); by default VSC's console is used

#### Windows

example of `launch.json`:

```json
{
    "configurations": [
        {
            "name": "C/C++: g++.exe build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\bin\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\Soft\\mingw64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "Set Disassembly Flavor to Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: g++.exe build active fila"
        }
    ],
    "version": "2.0.0"
}
```

#### Linux

example of `launch.json`:

```json
{
    "configurations": [
        {
            "name": "C/C++: g++ build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/bin/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "Set Disassembly Flavor to Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: g++ build active file",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ],
    "version": "2.0.0"
}
```

> Note: `preLaunchTask` must reference the build task (its **label**)

## 4. Build, run, debug

Build: `Ctrl+Shift+B`  
Run: `F5`

You can set breakpoints on the left side of code (`F9` or by mouse).