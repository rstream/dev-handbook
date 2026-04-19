# Git

[<- back](./index.md)

## SSH for GitHub (quick setup)

### 1. Create SSH key

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter to use default path (`~/.ssh/id_ed25519`), set passphrase if needed.

### 2. Start `ssh-agent` and add key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 3. Add public key to GitHub

Show public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy output, then add it on GitHub:
`Settings -> SSH and GPG keys -> New SSH key`

### 4. Check SSH access

```bash
ssh -T git@github.com
```

Expected result: successful authentication message from GitHub.

### 5. Clone repository via SSH

```bash
git clone git@github.com:<owner>/<repo>.git
```
