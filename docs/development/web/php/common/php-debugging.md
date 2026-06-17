# Debugging helpers in PHP

[← back](../index.md)

Use these helpers while developing to inspect values and write simple diagnostic messages.

## Summary

- [Dump a value](#dump-a-value) - `var_dump()` prints value and type
- [Print readable data](#print-readable-data) - `print_r()` prints arrays and objects in a compact form
- [Write to error log](#write-to-error-log) - `error_log()` writes a diagnostic message

## Dump a value

`var_dump()` shows both the type and the value.

```php
var_dump($user);
```

It is useful when type matters.

```php
var_dump($_POST['age'] ?? null);
```

## Print readable data

`print_r()` is often easier to read for arrays.

```php
print_r($items);
```

Inside an HTML page, wrap debug output in `<pre>`.

```php
<pre><?php print_r($items); ?></pre>
```

## Write to error log

`error_log()` writes a message to the PHP error log instead of printing it into the page.

```php
error_log('User was saved');
```

For arrays or objects, convert the value to a string first.

```php
error_log(print_r($user, true));
```
