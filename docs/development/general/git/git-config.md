# Configuring Git

[← back](index.md)

## Summary

- [Configuration levels](#configuration-levels)
- [User name and email](#user-name-and-email)
- [Default branch](#default-branch)
- [Default editor](#default-editor)
- [Line endings](#line-endings)
- [View configuration](#view-configuration)
- [Change or remove a setting](#change-or-remove-a-setting)

## Configuration levels

Git stores configuration at several levels:

- `--system` - settings for every user on the computer;
- `--global` - settings for the current user;
- `--local` - settings for the current repository (the default when run inside a repository).

Local settings override global settings, and global settings override system
settings.

## User name and email

Set the name and email that Git will write to new commits:

```bash
git config --global user.name "John Doe"
git config --global user.email "your_email@example.com"
```

Use the same email address that is associated with your Git hosting account
(GitHub, GitLab, and so on).

To use a different identity in one repository, run the commands from that
repository without `--global`:

```bash
git config --local user.name "Work Name"
git config --local user.email "work_email@example.com"
```

## Default branch

Set `main` as the initial branch name for new repositories:

```bash
git config --global init.defaultBranch main
```

## Default editor

Nano:
```bash
git config --global core.editor "nano" 
````

Vim:
```bash
git config --global core.editor "vim"
```

Visual Studio Code:
```bash
git config --global core.editor "code --wait"
```

## Line endings

Text files can use two common line-ending formats:

- `LF` (`\n`) - standard on Linux and macOS;
- `CRLF` (`\r\n`) - standard for many Windows tools.

The `core.autocrlf` setting controls how Git converts line endings:

| Value | On checkout | On commit | Common use |
| --- | --- | --- | --- |
| `true` | Converts `LF` to `CRLF` | Converts `CRLF` to `LF` | Windows when local tools require `CRLF` |
| `input` | Does not convert | Converts `CRLF` to `LF` | Linux, macOS, and modern cross-platform development |
| `false` | Does not convert | Does not convert | When `.gitattributes` or the editor fully controls line endings |

Set the desired value globally:

```bash
git config --global core.autocrlf true
git config --global core.autocrlf input
git config --global core.autocrlf false
```

Run only one of these commands. A common choice is `true` on Windows and
`input` on Linux or macOS. If all development tools on Windows support `LF`,
using `input` there also avoids rewriting files to `CRLF` on checkout.

### Repository rules

For a shared repository, define line endings in `.gitattributes` instead of
relying only on each developer's global Git configuration:

```gitattributes
* text=auto eol=lf
```

This stores and checks out text files with `LF`. Files that specifically
require `CRLF`, such as Windows batch scripts, can be configured separately:

```gitattributes
*.bat text eol=crlf
*.cmd text eol=crlf
```

Repository rules in `.gitattributes` take precedence over `core.autocrlf` for
matching files.

## View configuration

Show all effective settings and the files they come from:

```bash
git config --list --show-origin
```

Show settings for a specific level:

```bash
git config --global --list
git config --local --list
```

Show one setting:

```bash
git config user.name
git config user.email
```

## Change or remove a setting

Running `git config` again replaces the current value:

```bash
git config --global user.name "New Name"
```

Remove a setting:

```bash
git config --global --unset user.name
```

Configuration files can also be opened in the default editor:

```bash
git config --global --edit
git config --local --edit
```
