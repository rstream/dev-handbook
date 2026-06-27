# OPI

[← back](../index.md)

OPI (OBS Package Installer) is a tool that allows to install packages from the community repositories.  

## Install OPI

```bash
sudo zypper install opi
```

## Search and install packages

Example: find all packages which name includes `doublecmd`.
```bash
opi doublecmd
```
* will list matching packages with ability to choose one of them
* will ask to add new repository for the package (if not yet added)
