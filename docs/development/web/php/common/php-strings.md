# Strings in PHP

[← back](../index.md)

Strings store text data.
Use them for plain text, formatted messages, paths, HTML fragments, and other text values.

## Summary

- [Define strings](#define-strings) - single and double quotes
- [Concatenate strings](#concatenate-strings) - join text with `.`
- [Interpolate variables](#interpolate-variables) - insert variables into double-quoted strings
- [Access string length](#access-string-length) - `strlen()` counts characters
- [Trim whitespace](#trim-whitespace) - `trim()` removes leading and trailing spaces
- [Change case](#change-case) - `strtoupper()` and `strtolower()` change letter case
- [Format a string](#format-a-string) - `sprintf()` builds formatted text

## <a id="define-strings"></a>Define strings

```php
$name = 'Alice';
$message = "Hello, world";
```

Single quotes create a literal string.
Double quotes allow variable interpolation and escape sequences like `\n`.

## <a id="concatenate-strings"></a>Concatenate strings

```php
$fullName = $firstName . ' ' . $lastName;
```

## <a id="interpolate-variables"></a>Interpolate variables

```php
$message = "Hello, $name";
$title = "User: {$user['name']}";
```

## <a id="access-string-length"></a>Access string length

```php
$len = strlen($message);
```

## <a id="trim-whitespace"></a>Trim whitespace

```php
$title = trim($title);
```

## <a id="change-case"></a>Change case

```php
$upper = strtoupper($name);
$lower = strtolower($name);
```

## <a id="format-a-string"></a>Format a string

```php
$text = sprintf('%s has %d messages', $name, $count);
```
