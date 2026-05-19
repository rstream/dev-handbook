# Random values in PHP

[← back](../index.md)

Use PHP random helpers when you need random numbers, tokens, or identifiers.
Use cryptographically secure helpers for passwords, reset links, sessions, and API tokens.

## Summary

- [Random integer](#random-integer) - `random_int()` returns a secure random integer in a range
- [Random bytes](#random-bytes) - `random_bytes()` returns secure random bytes
- [Readable random token](#readable-random-token) - `bin2hex()` converts random bytes to a readable token

## Random integer

`random_int()` returns a cryptographically secure integer between two inclusive limits.

```php
$code = random_int(100000, 999999);
```

Use it for verification codes or security-sensitive random numbers.

## Random bytes

`random_bytes()` returns raw random bytes.

```php
$bytes = random_bytes(32);
```

Raw bytes are not always safe to print or put into a URL directly.
Convert them to text first.

## Readable random token

`bin2hex()` converts bytes to hexadecimal text.
This is a common way to create tokens.

```php
$token = bin2hex(random_bytes(32));
```

`32` bytes become a 64-character hex string.
