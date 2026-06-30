# `$_SERVER` in PHP

[← back](../index.md)

`$_SERVER` contains server and request information. For HTTP requests, it is commonly used to read the request method, URL path, query string, host, and headers.

## Summary

- [Request method](#request-method) - read `GET`, `POST`, and other HTTP methods
- [Path and query string](#path-and-query-string) - read the current URL parts
- [Host and protocol](#host-and-protocol) - read basic request location info
- [Headers](#headers) - read selected request headers
- [Route by method and path](#route-by-method-and-path) - handle different requests

## Request method

The current HTTP method is stored in `REQUEST_METHOD`.

```php
$method = $_SERVER['REQUEST_METHOD'];

if ($method === 'GET') {
    echo 'This is a GET request';
}

if ($method === 'POST') {
    echo 'This is a POST request';
}
```

Common methods:

- `GET` - read data
- `POST` - send form data or create data
- `PUT` - replace data
- `PATCH` - update part of data
- `DELETE` - delete data

## Path and query string

`REQUEST_URI` contains the path and query string.

```php
$requestUri = $_SERVER['REQUEST_URI'];

echo $requestUri;
```

For this URL:

```text
/products.php?category=laptops&page=2
```

`REQUEST_URI` contains:

```text
/products.php?category=laptops&page=2
```

Use `parse_url()` to read only the path:

```php
$path = parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH);

echo $path;
```

Result:

```text
/products.php
```

The raw query string is stored in `QUERY_STRING`.

```php
$queryString = $_SERVER['QUERY_STRING'] ?? '';
```

For parsed query parameters, use [`$_GET`](php-req-get.md).

## Host and protocol

Common values:

```php
$host = $_SERVER['HTTP_HOST'] ?? '';
$protocol = $_SERVER['SERVER_PROTOCOL'] ?? '';
```

Example output:

```text
localhost:8000
HTTP/1.1
```

## Headers

Some request headers are available in `$_SERVER` with an `HTTP_` prefix.

```php
$userAgent = $_SERVER['HTTP_USER_AGENT'] ?? '';
$accept = $_SERVER['HTTP_ACCEPT'] ?? '';
```

For example, the `User-Agent` header becomes `HTTP_USER_AGENT`.

## Route by method and path

`$_SERVER` is often used to choose which code should handle the request.

```php
$method = $_SERVER['REQUEST_METHOD'];
$path = parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH);

if ($method === 'GET' && $path === '/products') {
    echo 'Product list';
    exit;
}

if ($method === 'POST' && $path === '/products') {
    echo 'Create product';
    exit;
}

http_response_code(404);
echo 'Not found';
```

## Notes

- `REQUEST_METHOD` is usually the first value to check when handling forms or API routes
- `REQUEST_URI` includes the query string
- `parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH)` returns only the path
- use `??` for optional values because not every server key is always present
- values from `$_SERVER` should not be trusted blindly if they come from request data, such as headers
