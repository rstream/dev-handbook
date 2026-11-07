# NVM

[← back](index.md)

NVM (Node Version Manager) manages multiple Node.js installations for one user.
These commands use [nvm-sh](https://github.com/nvm-sh/nvm) for Linux, macOS, and WSL with shells such as Bash or Zsh.
Native Windows uses a separate project, nvm-windows, with different commands.

## Summary

- [Check NVM](#check-nvm)
- [List versions](#list-versions)
- [Install versions](#install-versions)
- [Switch versions](#switch-versions)
- [Latest LTS](#latest-lts)
- [Default version](#default-version)
- [Project version](#project-version)
- [Run with another version](#run-with-another-version)
- [Global packages](#global-packages)
- [Remove versions](#remove-versions)

## Check NVM

Follow the official [installation instructions](https://github.com/nvm-sh/nvm#installing-and-updating), then reopen the terminal.

```bash
command -v nvm
nvm --version
nvm help
```

NVM is a shell function, so use `command -v nvm` to check availability.

## List versions

| Command | Result |
| --- | --- |
| `nvm ls` | Installed versions and aliases |
| `nvm ls-remote` | Versions available to download |
| `nvm ls-remote --lts` | Available LTS releases |
| `nvm current` | Active Node.js version |
| `node --version` | Version used by the `node` command |
| `npm --version` | Active npm version |
| `nvm which 24` | Path to the selected installed Node.js executable |

## Install versions

```bash
# Latest release in the 24.x line
nvm install 24

# An exact version (example)
nvm install 24.14.0

# Latest release, including non-LTS releases
nvm install node
```

Installation also activates the version in the current shell and includes npm.
Running `nvm install 24` again checks for a newer 24.x release; older installations remain available.

## Switch versions

```bash
nvm use 24
nvm use 24.14.0
```

`use` selects an installed version for the current shell. It does not download missing versions or change other open terminals.
A partial version such as `24` selects the newest installed matching version.

```bash
# Use Node.js installed outside NVM, if available
nvm use system

# Remove NVM's Node.js paths from this shell's PATH
nvm deactivate
```

## Latest LTS

LTS means Long-Term Support. Query the release list instead of hardcoding whichever version is currently the newest LTS.

```bash
# All published LTS versions
nvm ls-remote --lts

# Exact latest LTS version available remotely, without installing it
nvm version-remote --lts

# Download and activate the latest LTS
nvm install --lts

# Activate the LTS alias target (must already be installed)
nvm use --lts
```

For a specific LTS line, use its codename from `nvm ls-remote --lts`:

```bash
nvm install --lts=krypton
nvm use --lts=krypton
```

`nvm use --lts` does not update Node.js. Run `nvm install --lts` again to get newer LTS releases.
LTS aliases are refreshed when NVM queries remote releases; if an alias points to a missing version, install it first.

## Default version

The `default` alias chooses Node.js when a new shell loads NVM.

```bash
# Newest installed 24.x
nvm alias default 24

# Apply the default to this shell too
nvm use default

# Inspect the configured alias and its resolved version
nvm alias default
nvm version default
```

To follow the latest LTS alias instead:

```bash
nvm install --lts
nvm alias default 'lts/*'
nvm use default
```

The alias does not install updates automatically. Keep the target installed with `nvm install --lts`.
For a fixed default, use a full version such as `nvm alias default 24.14.0`.
Quote `'lts/*'` to prevent shell wildcard expansion.

> Note: to apply new default version to all new terminals - log out and log in back.

## Project version

Store the project's Node.js version in `.nvmrc` at the repository root:

```text
24.14.0
```

From that directory:

```bash
# Install and activate the version from .nvmrc
nvm install

# Activate it when already installed
nvm use
```

To pin the currently active version:

```bash
node --version > .nvmrc
```

Commit `.nvmrc` so teammates can select the same version.
It can also contain `24` or `lts/*`, but those allow the resolved version to change.
NVM searches the current directory and its parents for `.nvmrc`; changing directories alone does not switch versions without extra shell integration.

## Run with another version

```bash
# Run a script with an installed Node.js version
nvm run 24 app.js

# Run another command with that version in a subshell
nvm exec 24 npm test
```

These commands leave the parent shell's selected version unchanged.

## Global packages

Global npm packages belong to individual Node.js installations.

```bash
# Install a newer 24.x and copy global packages from the active version
nvm install 24 --reinstall-packages-from=current

# Copy global packages from an installed 22.x to the active version
nvm reinstall-packages 22
```

Project dependencies remain in the project's `node_modules` and are managed through `package.json`.

## Remove versions

Switch away from the version before removing it:

```bash
nvm use 24
nvm uninstall 22.22.1
```

Use the full installed version from `nvm ls`. Update `default` and project `.nvmrc` files if they reference the removed version.

Command reference: [NVM usage](https://github.com/nvm-sh/nvm#usage) and [built-in help](https://github.com/nvm-sh/nvm/blob/master/nvm.sh).
