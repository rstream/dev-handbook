# Node Static

[← back](../index.md)

`node-static` is a small package for serving static files from a directory.
It is useful for simple local servers, demos, and small projects without Express.

## Summary

- [Install](#install) - add `node-static` to the project
- [Folder structure](#folder-structure) - keep browser files in `public`
- [Disable cache](#disable-cache) - make browsers request static files again
- [Static files with GET and POST endpoints](#static-files-with-get-and-post-endpoints) - serve files and handle two API routes
- [Run server](#run-server) - start the server with Node.js

## Install

```bash
npm i node-static
```

## Folder structure

Example project:

```text
project/
  public/
    index.html
    app.js
    styles.css
  server.js
  package.json
```

Files from `./public` will be available in the browser.
For example, `./public/index.html` will be served as `/index.html`.

## Disable cache

By default, `node-static` sends `Cache-Control` with a one-hour lifetime. For local development, disable this default and send `no-store` so that the browser does not store static-file responses:

```js
const files = new staticServer.Server('./public', {
    cache: false,
    headers: {
        'Cache-Control': 'no-store',
    },
});
```

`cache: false` prevents `node-static` from setting its default cache duration, while `no-store` prevents the browser from saving subsequent responses. Files changed in `public` are served on the next request; restarting the server is not required. A response cached before this setting was enabled may need one hard reload or cleared site data.

## Static files with GET and POST endpoints

```js
import http from 'node:http';
import staticServer from 'node-static';

const files = new staticServer.Server('./public');

const server = http.createServer((req, res) => {
    if (req.method === 'GET' && req.url === '/api/hello') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: 'Hello from Node.js' }));
        return;
    }

    if (req.method === 'POST' && req.url === '/api/echo') {
        let body = '';

        req.on('data', (chunk) => {
            body += chunk;
        });

        req.on('end', () => {
            res.writeHead(200, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ received: body }));
        });

        return;
    }

    files.serve(req, res);
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
http://localhost:3000
```

Test the GET endpoint:

```bash
curl http://localhost:3000/api/hello
```

Test the POST endpoint:

```bash
curl -X POST http://localhost:3000/api/echo -d "hello"
```
