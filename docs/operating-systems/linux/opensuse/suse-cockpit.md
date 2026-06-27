# Cockpit for openSUSE

[← back](index.md)

Cockpit is a web-based GUI for Linux administration.

## Install Cockpit

```bash
sudo zypper install cockpit
```

You will get a warning about the conflict with "busybox-hostname".  
Choose deinstallation of "busybox-hostname".

## Enable Cockpit

Make Cockpit available on localhost:
```bash
sudo systemctl enable --now cockpit.socket
```

## Access Cockpit

Access Cockpit through the web browser:
```
https://localhost:9090
```
