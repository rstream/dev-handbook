# HTTP response codes in PHP

[← back](../index.md)

Use `http_response_code()` to set the HTTP status returned to the client.

## Summary

- [Set and read the status](#set-and-read-the-status)
- [Reject a request](#reject-a-request)
- [Redirect after a POST](#redirect-after-a-post)
- [Common status codes](#common-status-codes)

## Set and read the status

```php
http_response_code(404);
echo 'Not found';
exit;
```

Set the status and headers before sending any output, including HTML, `echo`, or whitespace outside PHP tags. In a web server environment, the default status is normally `200`.

Without an argument, `http_response_code()` reads the current status:

```php
http_response_code(201);
$status = http_response_code(); // 201
```

When setting a status, the function returns the previous status. Setting it does not stop the script or generate an error page: write the response body yourself and use `exit` when processing should end. Printing an error message alone does not set an error status.

## Reject a request

Return `405` when a resource does not accept the request method. Include an `Allow` header listing its supported methods:

```php
if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
    http_response_code(405);
    header('Allow: POST');
    echo 'Method not allowed';
    exit;
}
```

Return `403` when access is forbidden. Assuming `$canEdit` was computed by your authorization logic:

```php
if (!$canEdit) {
    http_response_code(403);
    echo 'Access denied';
    exit;
}
```

Use `401` when authentication is required or invalid; include a `WWW-Authenticate` challenge appropriate to your authentication scheme. Use `403` when the server refuses access, for example because an authenticated user lacks permission.

## Redirect after a POST

After successfully processing a form, redirect to a page with `303` so the client follows with a `GET`:

```php
header('Location: /products', true, 303);
exit;
```

The third argument to `header()` sets the status. A `Location` header alone normally produces `302`; choose an explicit code when the redirect behavior matters. Use `307` or `308` when the method and body must be preserved.

## Common status codes

Status families: `1xx` informational, `2xx` success, `3xx` redirection, `4xx` client errors, `5xx` server errors.

| Code | Name | Meaning / typical use |
| --- | --- | --- |
| `200` | OK | Successful request. |
| `201` | Created | Resource created; `Location` can identify it. |
| `202` | Accepted | Processing accepted but unfinished. |
| `204` | No Content | Success without a response body. |
| `301` | Moved Permanently | Permanent redirect; clients may change POST to GET. |
| `302` | Found | Temporary redirect; clients may change POST to GET. |
| `303` | See Other | Retrieve another URL, typically with GET after POST. |
| `304` | Not Modified | Conditional request: reuse cached content; no response body. |
| `307` | Temporary Redirect | Temporary redirect preserving method and body. |
| `308` | Permanent Redirect | Permanent redirect preserving method and body. |
| `400` | Bad Request | Invalid request. |
| `401` | Unauthorized | Authentication required or invalid; send `WWW-Authenticate`. |
| `403` | Forbidden | Access refused. |
| `404` | Not Found | Resource not found. |
| `405` | Method Not Allowed | Unsupported method for this resource; send `Allow`. |
| `409` | Conflict | Conflict with current resource state. |
| `413` | Content Too Large | Request body too large. |
| `415` | Unsupported Media Type | Unsupported request content format. |
| `422` | Unprocessable Content | Understood format, but invalid content or instructions. |
| `429` | Too Many Requests | Rate limit exceeded; `Retry-After` can indicate when to retry. |
| `500` | Internal Server Error | Unexpected server failure. |
| `502` | Bad Gateway | Gateway received an invalid upstream response. |
| `503` | Service Unavailable | Temporarily unavailable; may include `Retry-After`. |
| `504` | Gateway Timeout | Gateway timed out awaiting an upstream response. |

Do not send a response body with `204` or `304`. Responses to `HEAD` also have no body.

## References

- [PHP: http_response_code()](https://www.php.net/manual/en/function.http-response-code.php)
- [PHP: header()](https://www.php.net/manual/en/function.header.php)
- [HTTP status semantics (RFC 9110)](https://httpwg.org/specs/rfc9110.html#status.codes)
- [429 Too Many Requests (RFC 6585)](https://www.rfc-editor.org/rfc/rfc6585.html#section-4)
