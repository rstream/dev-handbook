# Google Chrome for Linux

[← back](../index.md)

## Install Chrome

### Using [OPI](../opensuse/suse-opi.md)

```bash
opi chrome
```

### Manually

```bash
# Add repo for Chrome
sudo zypper ar http://dl.google.com/linux/chrome/rpm/stable/x86_64 google-chrome
# Import GPG key
sudo rpm --import https://dl.google.com/linux/linux_signing_key.pub
# Refresh repo
sudo zypper ref google-chrome
# Install Chrome
sudo zypper install google-chrome-stable
```
