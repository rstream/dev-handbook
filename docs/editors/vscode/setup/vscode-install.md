# VS Code installation

[← back](../index.md)

## Windows

Download and install VS Code:  
https://code.visualstudio.com/download  

## Linux

### Install Using OPI

```sh
opi vscode
```

This would include GPG key import and repository addition.

### Manual installation

Download the GPG key (ASCII version):
```sh
sudo wget https://packages.microsoft.com/keys/microsoft.asc
```
Import the GPG key:
```sh
sudo rpm --import microsoft.asc
```

Add repository (and refresh):
```sh
sudo zypper addrepo https://packages.microsoft.com/yumrepos/vscode 
vscode
sudo zypper refresh
```

Install VS Code:
```sh
sudo zypper install code
```