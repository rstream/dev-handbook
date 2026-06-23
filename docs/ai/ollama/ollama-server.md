# Ollama server

[← back](index.md)

> Note: if you are using non-default location for storing models you need to set the `OLLAMA_MODELS` environment variable in order to run Ollama server from console (`ollama serve`).

## Start server

Run Ollama server for API access:

```bash
ollama serve
```

By default, the API is available at:

```text
http://localhost:11434
```

If the Ollama desktop app is already running, the server may already be
available and `ollama serve` is not required.

## Diagnostic curl

Check that the server responds:

```bash
curl http://localhost:11434/api/version
```

Expected result is a JSON response with the Ollama version, for example:

```json
{"version":"0.30.10"}
```

List local models through the API:

```bash
curl http://localhost:11434/api/tags
```

## Simple request

Send a simple prompt to a local model:

```bash
curl http://localhost:11434/api/generate -d "{\"model\":\"gemma4:e2b\",\"prompt\":\"What is the capital of Canada?\",\"stream\":false}"
```

`stream` set to true would generate response in a streamed mode (word by word).
