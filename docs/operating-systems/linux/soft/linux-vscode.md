# Visual Studio Code for Linux

[← back](../index.md)

## Fix icon for VS Code

VS Code does not put icon in the default icon folder (`/usr/share/icons`), but stores it in `/usr/share/pixmaps`. That's why some applications (like Double Commander), cannot find the icon (they do not search in `pixmaps` folder). That's why DC does not show the icon for VS Code.

How to fix: just copy the icon from `/usr/share/pixmaps` to `/usr/share/icons`.
```sh
# create a folder (if it does not exist)
mkdir -p ~/.local/share/icons/hicolor/256x256/apps
# copy the icon
cp /usr/share/pixmaps/vscode.png ~/.local/share/icons/hicolor/256x256/apps
```