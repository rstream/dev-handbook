# C++ compilers for Linux

[← back](../index.md)

## GCC/G++ compiler

Some old version (like 7) may be already installed, but you may have to install the new one.

Check for the available versions:

```sh
zypper info gcc??
```
Install the latest GCC/G++ from the official repo (let's say it's **v15**):

```sh
sudo zypper install gcc15
sudo zypper install gcc15-c++
```

Create symlinks to use `gcc` and `g++` in the command line (instead of `gcc-15`/`g++-15`):

```sh
sudo ln -s /usr/bin/gcc-14 /usr/bin/gcc
sudo ln -s /usr/bin/g++-14 /usr/bin/g++
```

## Clang

Clang is an alternative to GCC. It is faster and has more detailed logs and error messages.  
Also it is required for [Kate](../../editors/kate/index.md) to work with C++.

To install run:
```sh
sudo zypper install clang
sudo zypper install lldb
```
This would install:
* `clang` - the compiler itself
* `clangd` - LSP server
* `lldb` - debugger