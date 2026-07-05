# AJAX: streamed request

[в†ђ back](../index.md)

HTTP requests can be sent in parts. This is useful when you have to upload big data to the server.

## Summary

- [Server](#server) - receive text lines from the request stream
- [Client](#client) - send text lines as request chunks
- [Run](#run) - start the server and client

## Server

The server handles a `POST` request, reads text chunks from the request body, splits them into lines, and passes each line to another module. The module is only a placeholder here: its implementation is not important for the streaming example.

```js
import http from 'node:http';

const lineReceiver = {
    async send(line) {
        // Imagine that this sends the line to another service or module.
        console.log('received:', line);
    }
};

const server = http.createServer(async (req, res) => {
    const url = new URL(req.url, 'http://localhost');

    if (req.method === 'POST' && url.pathname === '/upload') {
        const decoder = new TextDecoder();

        let buffer = '';
        let count = 0;

        try {
            for await (const chunk of req) {
                buffer += decoder.decode(chunk, { stream: true });

                const lines = buffer.split('\n');
                buffer = lines.pop() || ''; // the last line may be partial - keep it in the buffer

                for (const line of lines) {
                    await lineReceiver.send(line);
                    count++;
                }
            }

            // the last "tail"
            buffer += decoder.decode();

            if (buffer) {
                await lineReceiver.send(buffer);
                count++;
            }

            res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
            res.end(`Upload finished. Lines received: ${count}`);
        } catch (error) {
            console.error(error);

            res.writeHead(500, { 'Content-Type': 'text/plain; charset=utf-8' });
            res.end('Upload failed');
        }

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

The client creates a `ReadableStream`, writes each string with a `\n` separator, and sends that stream as the request body.

```js
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

const body = new ReadableStream({
    async start(controller) {
        const encoder = new TextEncoder();

        for (const message of messages) {
            controller.enqueue(encoder.encode(`${message}\n`));
            await delay(1000);
        }

        controller.close();
    }
});

const response = await fetch('http://localhost:3000/upload', {
    method: 'POST',
    body,
    duplex: 'half'
});

console.log(await response.text());
```

`duplex: 'half'` is required by Node.js when a `fetch()` request uses a streaming body.

## Run

Start the server:

```bash
node server.js
```

Run the client in another terminal:

```bash
node client.js
```
