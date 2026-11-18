# Telegram for Linux

[← back](../index.md)

## Installation

### From official website

This is a preferred way since the repository version may be broken.

Download the app, unpack to `/opt` and create a symlink to `/usr/local/bin`:
```sh
wget -O telegram.tar.xz https://telegram.org/dl/desktop/linux
sudo tar -xf telegram.tar.xz -C /opt/
sudo ln -s /opt/Telegram/Telegram /usr/local/bin/telegram
```

### From repository or Discover

Can be easily installed via **Discover**.

Or from the official repository:
```bash
sudo zypper install telegram-desktop
```
