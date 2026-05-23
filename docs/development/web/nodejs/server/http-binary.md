# Binary data

[← back](../index.md)

Binary data is handled with `Buffer`.
Use it for files, images, archives, and raw byte payloads.

## Summary

- [Read binary body](#read-binary-body) - collect request chunks into a `Buffer`
- [POST binary data](#post-binary-data) - receive raw bytes
- [Return binary data](#return-binary-data) - send a `Buffer`
- [Return a file](#return-a-file) - stream a file from disk

## Read binary body

```js
function readBinaryBody(req) {
  return new Promise((resolve, reject) => {
    const chunks = [];

    req.on('data', (chunk) => {
      chunks.push(chunk);
    });

    req.on('end', () => {
      resolve(Buffer.concat(chunks));
    });

    req.on('error', reject);
  });
}
```

## POST binary data

```js
if (req.method === 'POST' && url.pathname === '/upload') {
  const data = await readBinaryBody(req);

  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({
    bytes: data.length
  }));
  return;
}
```

Request:

```bash
curl -X POST http://localhost:3000/upload -H "Content-Type: application/octet-stream" --data-binary "@image.png"
```

## Return binary data

```js
if (req.method === 'GET' && url.pathname === '/download') {
  const data = Buffer.from('Hello as bytes');

  res.writeHead(200, {
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="hello.bin"'
  });
  res.end(data);
  return;
}
```

## Return a file

Use `fs.createReadStream()` for real files, so Node.js does not need to load the whole file into memory.

```js
const fs = require('node:fs');

if (req.method === 'GET' && url.pathname === '/image') {
  res.writeHead(200, { 'Content-Type': 'image/png' });
  fs.createReadStream('./public/image.png').pipe(res);
  return;
}
```

Full example:

```js
const fs = require('node:fs');
const http = require('node:http');

function readBinaryBody(req) {
  return new Promise((resolve, reject) => {
    const chunks = [];

    req.on('data', (chunk) => {
      chunks.push(chunk);
    });

    req.on('end', () => {
      resolve(Buffer.concat(chunks));
    });

    req.on('error', reject);
  });
}

const server = http.createServer(async (req, res) => {
  const url = new URL(req.url, 'http://localhost');

  if (req.method === 'POST' && url.pathname === '/upload') {
    const data = await readBinaryBody(req);

    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ bytes: data.length }));
    return;
  }

  if (req.method === 'GET' && url.pathname === '/download') {
    const data = Buffer.from('Hello as bytes');

    res.writeHead(200, {
      'Content-Type': 'application/octet-stream',
      'Content-Disposition': 'attachment; filename="hello.bin"'
    });
    res.end(data);
    return;
  }

  if (req.method === 'GET' && url.pathname === '/image') {
    res.writeHead(200, { 'Content-Type': 'image/png' });
    fs.createReadStream('./public/image.png').pipe(res);
    return;
  }

  res.writeHead(404, { 'Content-Type': 'text/plain' });
  res.end('Not found');
});

server.listen(3000, () => {
  console.log('Server is running at http://localhost:3000');
});
```
