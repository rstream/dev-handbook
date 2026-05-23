# Text and JSON

[← back](../index.md)

HTTP requests and responses often send plain text or JSON.
For `POST` requests, read the request body from the `req` stream.

## Summary

**GET**
- [GET with text response](#get-with-text-response) - return plain text
- [GET with JSON response](#get-with-json-response) - return JSON

**POST**
- [Read request body](#read-request-body) - collect POST data as text
- [POST with text](#post-with-text) - receive and return text
- [POST with JSON](#post-with-json) - receive and return JSON

## GET

### GET with text response

```js
if (req.method === 'GET' && url.pathname === '/hello') {
  const name = url.searchParams.get('name') || 'Guest';

  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end(`Hello, ${name}`);
  return;
}
```

Request:

```bash
curl "http://localhost:3000/hello?name=Alice"
```

### GET with JSON response

```js
if (req.method === 'GET' && url.pathname === '/api/user') {
  const user = {
    id: 1,
    name: 'Alice'
  };

  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify(user));
  return;
}
```

Request:

```bash
curl http://localhost:3000/api/user
```

## POST

### Read request body

For `POST` requests, request data comes from the `req` stream.

```js
function readTextBody(req) {
  return new Promise((resolve, reject) => {
    let body = '';

    req.on('data', (chunk) => {
      body += chunk;
    });

    req.on('end', () => {
      resolve(body);
    });

    req.on('error', reject);
  });
}
```

### POST with text

```js
if (req.method === 'POST' && url.pathname === '/echo') {
  const body = await readTextBody(req);

  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end(`Received: ${body}`);
  return;
}
```

Request:

```bash
curl -X POST http://localhost:3000/echo -d "hello"
```

### POST with JSON

```js
if (req.method === 'POST' && url.pathname === '/api/user') {
  const body = await readTextBody(req);
  const user = JSON.parse(body);

  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({
    saved: true,
    user
  }));
  return;
}
```

Request:

```bash
curl -X POST http://localhost:3000/api/user -H "Content-Type: application/json" -d "{\"name\":\"Alice\"}"
```

Full example:

```js
const http = require('node:http');

function readTextBody(req) {
  return new Promise((resolve, reject) => {
    let body = '';

    req.on('data', (chunk) => {
      body += chunk;
    });

    req.on('end', () => {
      resolve(body);
    });

    req.on('error', reject);
  });
}

const server = http.createServer(async (req, res) => {
  const url = new URL(req.url, 'http://localhost');

  if (req.method === 'GET' && url.pathname === '/hello') {
    const name = url.searchParams.get('name') || 'Guest';

    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end(`Hello, ${name}`);
    return;
  }

  if (req.method === 'GET' && url.pathname === '/api/user') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ id: 1, name: 'Alice' }));
    return;
  }

  if (req.method === 'POST' && url.pathname === '/echo') {
    const body = await readTextBody(req);

    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end(`Received: ${body}`);
    return;
  }

  if (req.method === 'POST' && url.pathname === '/api/user') {
    const body = await readTextBody(req);
    const user = JSON.parse(body);

    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ saved: true, user }));
    return;
  }

  res.writeHead(404, { 'Content-Type': 'text/plain' });
  res.end('Not found');
});

server.listen(3000, () => {
  console.log('Server is running at http://localhost:3000');
});
```
