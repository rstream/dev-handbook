# C++ file compilation

[← back](index.md)

## Compile a single file

General syntax is:
```sh
g++ [options] [input files] [linker options] -o [output]
```

Build example:
```sh
g++ -g hello-again.cpp -o bin/hello 
```

Where:
* `-g` - add debug information ("exe" file would be bigger, not for production)
* `hello-again.cpp` - name of the input file
* `-o` - "output" flag (output file names goes after)
* `bin/hello` - name of the output file (e.g. "hello.exe" or "hello" in the folder "bin")

## Compile multiple files

Compile multiple files (headers are in the same folder):
```sh
g++ -g util.cpp app.cpp -o bin/hello
```

Compile multiple files (headers are in `./include`):
```sh
g++ -g util.cpp app.cpp -Iinclude -o bin/hello
```

## Additional compilation parameters

Build with additional parameters:
```sh
g++ -g -std=c++17 -Wall -Werror -pedantic -fdiagnostics-color=always hello-again.cpp -o bin/hello
```

Where:
* `-std=c++17` - set C++ standard for compiler; 17 is a good & stable standard for learning
* `-Wall` - enable all warnings
* -`Werror` - turn warnings into errors (will not compile project with warning) - to avoid unstable builds
* `-pedantic` - restrict compiler-specific features - 100% compatibility with C++ standard (version 17 in our case)
* `-fdiagnostics-color=always` - colorize terminal output

You can use `gcc` (used for pure "C" code) instead of `g++`, but need to add additional flag, since c++ library (`libstdc++`) is not enabled by default:
```sh
gcc -g -lstdc++ hello-again.cpp -o hello 
```
Still `g++` is recommended since it supports all C++ capabilities out of the box without additional flags.