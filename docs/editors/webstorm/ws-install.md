# Webstorm installation

[← back](index.md)

## Windows

Download and install Webstorm:  
https://www.jetbrains.com/webstorm/download/?section=windows

## Linux

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

Copy Webstorm to `/opt/webstorm`:
```sh
sudo rm -rf /opt/webstorm
sudo mv WebStorm-* /opt/webstorm
```

Run Webstorm:
```sh
/opt/webstorm/bin/webstorm.sh
```

Create a terminal launcher:
```sh
sudo ln -sf /opt/webstorm/bin/webstorm.sh /usr/local/bin/webstorm
```

Run Webstorm from the console:
```sh
webstorm
```
