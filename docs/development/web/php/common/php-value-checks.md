# Value checks in PHP

[← back](../index.md)

PHP has several common helpers and language constructs for checking values.
Use them to distinguish missing data, empty data, and values of a specific type.

## Summary

- [Check that a value exists](#check-that-a-value-exists) - `isset()` checks that a variable or key exists and is not `null`
- [Check for empty values](#check-for-empty-values) - `empty()` checks common empty values
- [Compare with `null`](#compare-with-null) - `=== null` and `!== null` are explicit null checks
- [Check value type](#check-value-type) - `is_string()`, `is_int()`, `is_float()`, `is_bool()`, `is_array()`, `is_object()`, and `is_null()`

## Check that a value exists

`isset()` returns `true` when a variable or array key exists and its value is not `null`.

```php
if (isset($_GET['page'])) {
    $page = (int) $_GET['page'];
}
```

It is useful for optional request parameters and optional array keys.

```php
if (isset($user['email'])) {
    echo $user['email'];
}
```

## Check for empty values

`empty()` returns `true` for missing variables and for values PHP considers empty, such as `''`, `'0'`, `0`, `false`, `null`, and `[]`.

```php
if (empty($name)) {
    echo 'Name is required';
}
```

Use `empty()` when this broad meaning is intended.
Use a stricter check when `0` or `'0'` should be allowed.

## Compare with `null`

Use strict comparison when you specifically need to check for `null`.

```php
if ($email === null) {
    echo 'Email is missing';
}

if ($email !== null) {
    echo $email;
}
```

## Check value type

Use `is_*()` helpers when code accepts mixed data and needs to branch by type.

```php
if (is_string($value)) {
    echo strtoupper($value);
}

if (is_array($value)) {
    echo count($value);
}
```

Common checks:

| Function | Checks |
| --- | --- |
| `is_string()` | string |
| `is_int()` | integer |
| `is_float()` | floating point number |
| `is_bool()` | boolean |
| `is_array()` | array |
| `is_object()` | object |
| `is_null()` | `null` |
