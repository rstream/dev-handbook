# Streamed text

[← back](../index.md)

HTTP responses can be sent in parts. This is useful when the server produces data gradually and the client should process it before the full response is finished.

## Summary

- [Server](#server) - send text lines with a delay
- [Client](#client) - read response lines with a stream reader
- [Run](#run) - start the server and client

## Server

The server handles a `POST` request and sends each string as a separate `text/plain` line.

```js
import http from 'node:http';

const messages = [
    'first line',
    'second line',
    'third line'
];

function delay(ms) {
    return new Promise((resolve) => {
        setTimeout(resolve, ms);
    });
}

const server = http.createServer(async (req, res) => {
    const url = new URL(req.url, 'http://localhost');

    if (req.method === 'POST' && url.pathname === '/stream') {
        res.writeHead(200, {
            'Content-Type': 'text/plain; charset=utf-8',
            'Cache-Control': 'no-cache'
        });

        for (const message of messages) {
            res.write(`${message}\n`);
            await delay(1000);
        }

        res.end();
        return;
    }

    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
});

server.listen(3000, () => {
    console.log('Server is running at http://localhost:3000');
});
```

## Client

The client sends a `POST` request, reads response chunks through `reader`, splits them into lines, and prints each line to the console.

```js
const response = await fetch('http://localhost:3000/stream', {
    method: 'POST',
    body: 'start'
});

if (!response.body) {
    throw new Error('Response body is not readable');
}

const reader = response.body.getReader();
const decoder = new TextDecoder();

let buffer = '';

while (true) {
    const { value, done } = await reader.read();

    if (done) {
        // the last "tail"
        buffer += decoder.decode();

        if (buffer) {
            console.log(buffer);
        }
        break;
    }

    buffer += decoder.decode(value, { stream: true });

    const lines = buffer.split('\n');
    buffer = lines.pop() || ''; // the last line may be partial - keep it in the buffer

    for (const line of lines) {
        console.log(line);
    }
}
```

## Run

Start the server:

```bash
node server.js
```

Run the client in another terminal:

```bash
node client.js
```
