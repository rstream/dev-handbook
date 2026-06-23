# HTTP server

[← back](../index.md)

Node.js can create an HTTP server without extra packages using the built-in `node:http` module.

## Summary

- [Create server](#create-server) - minimal HTTP server
- [Request and response](#request-and-response) - basic `req` and `res` fields
- [Route by method and path](#route-by-method-and-path) - handle different URLs
- [Run server](#run-server) - start the server

## Create server

```js
import http from 'node:http';

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello from Node.js');
});

server.listen(3000, () => {
    console.log('Server is running at http://localhost:3000');
});
```

## Request and response

`req` contains data about the incoming request:

- `req.method` - HTTP method, for example `GET` or `POST`
- `req.url` - path and query string, for example `/users?id=10`
- `req.headers` - request headers

`res` is used to send the response:

- `res.writeHead(status, headers)` - set status code and headers
- `res.end(data)` - finish response and send data

## Route by method and path

Use `URL` to read the path and query parameters.

```js
import http from 'node:http';

const server = http.createServer((req, res) => {
    const url = new URL(req.url, 'http://localhost');

    if (req.method === 'GET' && url.pathname === '/') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Home page');
        return;
    }

    if (req.method === 'GET' && url.pathname === '/hello') {
        const name = url.searchParams.get('name') || 'Guest';

        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end(`Hello, ${name}`);
        return;
    }

    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
});

server.listen(3000, () => {
    console.log('Server is running at http://localhost:3000');
});
```

## Run server

```bash
node server.js
```

Open:

```text
http://localhost:3000/hello?name=Alice
```
