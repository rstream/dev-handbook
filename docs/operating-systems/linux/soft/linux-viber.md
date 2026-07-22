# Viber for Linux

[← back](../index.md)

## Installation

Visit Viber website: https://www.viber.com/en/download/  
Select "Download for AppImage".

Copy "viber.appimage" to "~/Applications" and make it executable.
```bash
cp ~/downloads/viber.appimage ~/Applications
chmod +x ~/Applications/viber.appimage
```

## Make a shortcut

### Extract icon

Unpack Viber appimage:
```bash
./viber.appimage --appimage-extract
```

In the `squashfs-root` find "viber.png" and copy it to the `~/.local/share/icons/` directory.

### Create a .desktop file

Create "viber.desktop" file and make it executable.

> Note: you can find it in `squashfs-root`, just adjust the application and icon paths.

```
[Desktop Entry]
Type=Application
Name=Viber
Comment=Viber desktop
Exec=/home/user/Applications/viber.appimage
Icon=/home/user/.local/share/icons/viber.png
Terminal=false
Categories=Network;InstantMessaging;
MimeType=x-scheme-handler/viber;
StartupNotify=true
X-AppImage-Version=27.3.0.2
```

Copy it to:
1. Start menu folder: `~/.local/share/applications/`
2. Desktop folder: `~/Desktop/`
> Note: automatic updates are not available for Linux.
