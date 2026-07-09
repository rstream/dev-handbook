# Ollama basic commands

[← back](index.md)

## Download model

Download default version of the `gemma4` model
```bash
ollama pull gemma4
```

Notes:
* see the list of available models: https://ollama.com/library
* check which size is default: https://ollama.com/library/gemma4

Download `gemma4` in a specific size (`12B`):
```bash
ollama pull gemma4:12b
```

## Remove model

```bash
ollama rm gemma4
```

## Run model

### Interactive chat

To run a chat in terminal:
```bash
ollama run gemma4
```

### Server
Run server for API access

```bash
ollama serve
```

> Note: if your models are not in the default location (`C:\Users\<user>\.ollama\models`) - the environment variable `OLLAMA_MODELS` should be set (path to the folder with models, e.g. `D:\ai-models`)

## List models

```bash
ollama ls
```

## List running models

```bash
ollama ps
```

## Stop running model

```bash
ollama stop gemma4
```

