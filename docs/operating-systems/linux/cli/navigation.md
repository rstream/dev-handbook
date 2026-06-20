# CLI navigation

[← back](../index.md)

Basic commands for navigating directories in terminal.

## Current directory

```sh
pwd  # show the current working directory
```

## List files

```sh
ls      # list files
ls -l   # list files in long format
ls -a   # include hidden files
ls -h   # show human-readable file sizes
ls -la  # long format + hidden files
ls -lh  # long format + human-readable file sizes
```

List files in a specific directory:

```sh
ls /path/to/directory  # list files in absolute path
ls Documents           # list files in relative path
ls ..                  # list files in parent directory
ls ~                   # list files in home directory
ls -la /etc            # list files in /etc with options
```

## Change directory

```sh
cd Documents           # go to relative path
cd /path/to/directory  # go to absolute path
cd ..                  # go one level up
cd ../..               # go two levels up
cd ~                   # go to home directory
cd -                   # go to previous directory
```

## Path shortcuts

```sh
/   # root directory
.   # current directory
..  # parent directory
~   # home directory
```

## Path types

```sh
/home/user/projects  # absolute path
projects/app         # relative path
./script.sh          # file in current directory
../config            # path from parent directory
~/.config            # path inside home directory
```
