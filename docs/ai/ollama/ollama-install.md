# Ollama installation

[← back](index.md)

## Installation

### Windows

Download installer:
```
https://ollama.com/download/OllamaSetup.exe
```

or install from PowerShell:

```powershell
irm https://ollama.com/install.ps1 | iex
```

#### Set environment variable for models folder

If you are using non-default location for storing models you need to set the `OLLAMA_MODELS` environment variable in order to run Ollama server from console (`ollama serve`).

```bash
setx OLLAMA_MODELS "D:\ai-models"
```

### Linux

Install:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

## Check version

```sh
ollama -v
```

> Note: you will get a warning if neither Ollama GUI app nor Ollama Server is running.
