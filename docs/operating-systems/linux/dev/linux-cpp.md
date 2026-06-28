# C++ compilers for Linux

[← back](../index.md)

## GCC/G++ compiler

### Install GCC

Some old version (like 7) may be already installed, but you may have to install the new one.

Check for the available versions:

```sh
zypper info gcc??
```

Install the latest GCC/G++ from the official repo:
```sh
sudo zypper install gcc gcc-c++
```

On openSUSE 16 there's an issue: on fresh system installation the `cpp15` library version is `15.3` but GCC/G++ has only `15.2` on board.

> Solution: choose **"downgrade to 15.2"** during the installation.

### Create symlinks

There's a chance that `gcc`/`g++` commands are not available or pointing to the wrong (older) versions. In this case you need to create symlinks to the new installed versions of GCC / G++.
How to check:
```bash
ls -l "$(which gcc)"
ls -l "$(which g++)"
```

If outputs are pointing to the new versions (let's say - `15`) - you are good:
```
lrwxrwxrwx. 1 root root 6 Mar 12  2025 /usr/bin/gcc -> gcc-15
lrwxrwxrwx. 1 root root 6 Mar 12  2025 /usr/bin/g++ -> g++-15
```

If `gcc`/`g++` are not available or pointing to the older versions - you need to create symlinks.

#### update-alternatives

Good way to create a symlink (via `update-alternatives`):
```sh
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-15 100
```

Command description:

* `/usr/bin/g++` - path to "common" binary
* `g++` - group name (for switching between versions)
* `/usr/bin/g++-15` - path to real binary
* `100` - priority

To check all versions:  

```
sudo update-alternatives --display g++
```

#### Manual way

Manual way for symlink creation:

```sh
sudo ln -s /usr/bin/gcc-15 /usr/bin/gcc
sudo ln -s /usr/bin/g++-15 /usr/bin/g++
```

## Clang

Clang is an alternative to GCC. It is faster and has more detailed logs and error messages.  
Also it is required for [Kate](../../../editors/kate/index.md) to work with C++.

To install run:
```sh
sudo zypper install clang lldb
```

This would install:
* `clang` - the compiler itself
* `clangd` - LSP server
* `lldb` - debugger
