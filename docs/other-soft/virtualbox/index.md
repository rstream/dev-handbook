# VirtualBox

[← back](../../index.md)

## Installation

### Linux

Install VirtualBox from the official repository:
```sh
sudo zypper install virtualbox
```

Add yourself to the `vboxusers` group (system restart required, logout/login may be not enough)
```sh
sudo usermod -aG vboxusers $USER
```
