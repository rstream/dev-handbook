# CLI command basics

[← back](../index.md)

Basic principles of console command syntax.

## Command structure

```sh
command [options] [arguments]  # general syntax
ls -la /home/user              # command + options + argument
cp source.txt target.txt       # command + source argument + target argument
grep -i "text" file.txt        # command + option + search text + file argument
```

## Options

Short options usually start with one dash:

```sh
ls -l  # long format
ls -a  # include hidden files
ls -h  # human-readable file sizes
```

Some short options can be combined:

```sh
ls -l -a -h  # separate short options
ls -lah      # same options combined
```

Long options usually start with two dashes:

```sh
ls --all             # include hidden files
ls --human-readable  # human-readable file sizes
```

## Options with values

Some options require a value:

```sh
grep -n "text" file.txt  # show line numbers
head -n 20 file.txt      # show first 20 lines
```

Long options may use a space or `=`:

```sh
command --option value  # value separated by space
command --option=value  # value separated by =
```

## Getting help

Most commands support one of these:

```sh
command --help  # show short help
command -h      # show short help, if supported
ls --help       # show help for ls
grep --help     # show help for grep
```

Open a full manual page:

```sh
man command  # open full manual page
man ls       # open manual for ls
man grep     # open manual for grep
```

## Stop parsing options

Use `--` to tell a command that everything after it is an argument, not an option.

```sh
rm -- -file.txt  # remove file named "-file.txt"
```

Useful when a file name starts with `-`.

## Spaces in arguments

Use quotes when an argument contains spaces:

```sh
cd "My Documents"          # directory name contains a space
grep "hello world" file.txt  # search text contains a space
```

## Command examples in manuals

`$` usually means a regular user shell prompt:

```sh
$ ls  # run as regular user
```

`#` usually means a root shell prompt:

```sh
# zypper install package-name  # run as root
```

Do not copy `$` or `#` as part of the command.
