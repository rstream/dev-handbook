# ChatGPT installation on openSUSE

[← back](index.md)

ChatGPT desktop app has no repository for openSUSE, still you can manually download and install `rpm` package.  
More information here: https://learn.chatgpt.com/docs/linux/linux-app

## Download

Download package for Fedora
```sh
wget https://persistent.oaistatic.com/codex-app-prod/linux/rpm/latest/chatgpt.x86_64.rpm
```

##  Install the package

```sh
sudo zypper install chatgpt.x86_64.rpm
```

Notes:
* you'll be notified that GPG key is missing - ignore it
* repository will not be added, so update via package manager will not be available

## Run

Run via menu or by command
```sh
chatgpt
```