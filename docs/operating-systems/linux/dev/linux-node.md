# Node.js for Linux

[← back](../index.md)

## Install nvm

Visit the official page on GitHub:  
https://github.com/nvm-sh/nvm

In the `readme.md` you will find commands for installing the latest version:  
https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating

Commands are identical, use either of them:

curl:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.5/install.sh | bash
```

wget:
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.5/install.sh | bash
```

> note: restart the terminal to start using `nvm`

## Install Node.js

Install latest nodejs:
```bash
nvm install node
```

Check the node version:
```bash
node -v
```

Node.js may not work because of the missing dependency - `libatomic1`:
```bash
sudo zypper install libatomic1
```
