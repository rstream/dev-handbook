# C++ file compilation

[← back](index.md)

Build from command line:
```sh
g++ hello-again.cpp -o bin/hello -g -std=c++17 -Wall -Werror -pedantic -fdiagnostics-color=always
```

Where:

* `hello-again.cpp` - name of the input file
* `-o` - "output" flag (output file names goes after)
* `bin/hello` - name of the output file (e.g. "hello.exe" or "hello" in the folder "bin")
* `-g` - add debug information ("exe" file would be bigger, not for production)

And some optiona parameters:

* `-std=c++17` - set C++ standard for compiler; 17 is a good & stable standard for learning
* `-Wall` - enable all warnings
* -`Werror` - turn warnings into errors (will not compile project with warning) - to avoid unstable builds
* `-pedantic` - restrict compiler-specific features - 100% compatibility with C++ standard (version 17 in our case)
* `-fdiagnostics-color=always` - colorize terminal output

You can use "gcc" (used for pure "C" code) instead of "g++", but need to add additional flag, since c++ library (libstdc++) is not enabled by default:
```sh
gcc -o hello hello-again.cpp -g -lstdc++
```

> still g++ is recommended since it supports all C++ capabilities out of the box without additional flags.