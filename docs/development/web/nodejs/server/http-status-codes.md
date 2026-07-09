# Status codes

[← back](../index.md)

HTTP status code tells the client what happened with the request.
In Node.js, set it before sending the response body.

## Summary

- [Status code classes](#status-code-classes) - groups of HTTP status codes
- [Common status codes](#common-status-codes) - codes used most often
- [Set status code](#set-status-code) - send a status with `node:http`
- [Success responses](#success-responses) - `200`, `201`, and `204`
- [Client error responses](#client-error-responses) - `400`, `401`, `403`, `404`, and `405`
- [Server error responses](#server-error-responses) - `500`
- [Full example](#full-example) - small API with different statuses

## Status code classes

| Class | Meaning | Example |
| --- | --- | --- |
| `1xx` | Informational response | `100 Continue` |
| `2xx` | Request succeeded | `200 OK` |
| `3xx` | Redirect | `301 Moved Permanently` |
| `4xx` | Client error | `404 Not Found` |
| `5xx` | Server error | `500 Internal Server Error` |

Most simple API servers use mainly `2xx`, `4xx`, and `5xx`.

## Common status codes

| Code | Meaning | When to use |
| --- | --- | --- |
| `200 OK` | Request succeeded | Return data for a successful `GET` request |
| `201 Created` | New resource was created | Successful `POST` that creates data |
| `204 No Content` | Request succeeded, no body | Successful `DELETE` or update without response data |
| `301 Moved Permanently` | Permanent redirect | URL was changed permanently |
| `302 Found` | Temporary redirect | Send client to another URL temporarily |
| `400 Bad Request` | Invalid request | Missing fields or invalid JSON |
| `401 Unauthorized` | Authentication required | User is not logged in |
| `403 Forbidden` | Access denied | User is known but has no permission |
| `404 Not Found` | Resource not found | Unknown URL or missing item |
| `405 Method Not Allowed` | Wrong HTTP method | Path exists, but method is not supported |
| `500 Internal Server Error` | Server failed | Unexpected error in server code |

## Set status code

Use `res.writeHead()` to set status code and headers together.

```js
res.writeHead(200, { 'Content-Type': 'text/plain' });
res.end('OK');
```

Or set `res.statusCode` before `res.end()`.

```js
res.statusCode = 404;
res.setHeader('Content-Type', 'text/plain');
res.end('Not found');
```

## Success responses

### 200 OK

Use `200` when the request succeeded and the response has data.

```js
if (req.method === 'GET' && url.pathname === '/api/user') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ id: 1, name: 'Alice' }));
    return;
}
```

### 201 Created

Use `201` when a `POST` request creates a new resource.

```js
if (req.method === 'POST' && url.pathname === '/api/users') {
    res.writeHead(201, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ id: 2, name: 'Bob' }));
    return;
}
```

### 204 No Content

Use `204` when the request succeeded but there is no response body.

```js
if (req.method === 'DELETE' && url.pathname === '/api/user') {
    res.writeHead(204);
    res.end();
    return;
}
```

Do not send a body with `204`.

## Client error responses

### 400 Bad Request

Use `400` when the client sends invalid data.

```js
if (!name) {
    res.writeHead(400, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ error: 'Name is required' }));
    return;
}
```

### 401 Unauthorized

Use `401` when authentication is required.

```js
if (!req.headers.authorization) {
    res.writeHead(401, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ error: 'Authentication required' }));
    return;
}
```

### 403 Forbidden

Use `403` when the client is authenticated but not allowed to access the resource.

```js
if (user.role !== 'admin') {
    res.writeHead(403, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ error: 'Access denied' }));
    return;
}
```

### 404 Not Found

Use `404` when the route or resource does not exist.

```js
res.writeHead(404, { 'Content-Type': 'application/json' });
res.end(JSON.stringify({ error: 'Not found' }));
```

### 405 Method Not Allowed

Use `405` when the path exists but the HTTP method is not supported.

```js
if (url.pathname === '/api/user') {
    res.writeHead(405, {
        'Content-Type': 'application/json',
        'Allow': 'GET, DELETE'
    });
    res.end(JSON.stringify({ error: 'Method not allowed' }));
    return;
}
```

The `Allow` header lists methods supported by this path.

## Server error responses

### 500 Internal Server Error

Use `500` when the server has an unexpected error.

```js
try {
    const user = await loadUserFromDatabase();

    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(user));
} catch (error) {
    res.writeHead(500, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ error: 'Internal server error' }));
}
```

Do not send internal error details to the client in production.

## Full example

```js
import http from 'node:http';

function sendJson(res, statusCode, data) {
    res.writeHead(statusCode, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(data));
}

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

const users = [
    { id: 1, name: 'Alice' }
];

const server = http.createServer(async (req, res) => {
    const url = new URL(req.url, 'http://localhost');

    try {
        if (url.pathname === '/api/users' && req.method === 'GET') {
            sendJson(res, 200, users);
            return;
        }

        if (url.pathname === '/api/users' && req.method === 'POST') {
            const body = await readTextBody(req);
            let data;

            try {
                data = JSON.parse(body);
            } catch (error) {
                sendJson(res, 400, { error: 'Invalid JSON' });
                return;
            }

            if (!data.name) {
                sendJson(res, 400, { error: 'Name is required' });
                return;
            }

            const user = {
                id: users.length + 1,
                name: data.name
            };

            users.push(user);
            sendJson(res, 201, user);
            return;
        }

        if (url.pathname === '/api/users') {
            res.writeHead(405, {
                'Content-Type': 'application/json',
                'Allow': 'GET, POST'
            });
            res.end(JSON.stringify({ error: 'Method not allowed' }));
            return;
        }

        sendJson(res, 404, { error: 'Not found' });
    } catch (error) {
        sendJson(res, 500, { error: 'Internal server error' });
    }
});

server.listen(3000, () => {
    console.log('Server is running at http://localhost:3000');
});
```

Requests:

```bash
curl http://localhost:3000/api/users
curl -X POST http://localhost:3000/api/users -H "Content-Type: application/json" -d "{\"name\":\"Bob\"}"
curl -X POST http://localhost:3000/api/users -H "Content-Type: application/json" -d "{}"
curl -X DELETE http://localhost:3000/api/users
```
