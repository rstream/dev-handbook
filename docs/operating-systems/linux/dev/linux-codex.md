# Codex installation

[← back](../index.md)

## Codex app on Linux

The Codex desktop app is available for macOS and Windows. On Linux, use the Codex CLI.

## Install codex CLI

Install Codex:

```sh
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Run Codex:

```sh
codex
```

## Sandbox dependency

Codex uses `bubblewrap` for sandboxing on Linux. Install it with your package manager.

```sh
sudo zypper install bubblewrap
```

