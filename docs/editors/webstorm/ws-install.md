# Webstorm installation

[← back](index.md)

## Windows

Download and install Webstorm:  
https://www.jetbrains.com/webstorm/download/?section=windows

## Linux

### Download/unpack

Download Webstorm for Linux (tar.gz):  
https://www.jetbrains.com/webstorm/download/?section=linux

Go to the directory with the downloaded archive:
```sh
cd ~/Downloads
```

Unpack the archive:
```sh
tar -xzf WebStorm-*.tar.gz
```

### Move to `/opt/webstorm` and make a test run

Move unpacked Webstorm files to `/opt/webstorm`:
```sh
sudo rm -rf /opt/webstorm
sudo mv WebStorm-* /opt/webstorm
```

Run Webstorm:
```sh
/opt/webstorm/bin/webstorm
```

### Create a symlink and start menu entry

Create a symlink:
```sh
sudo ln -sf /opt/webstorm/bin/webstorm /usr/local/bin/webstorm
```

Run Webstorm from the console:
```sh
webstorm
```

Create a start menu entry:

Copy this [desktop file](assets/webstorm.desktop) to:  
`~/.local/share/applications/webstorm.desktop`
