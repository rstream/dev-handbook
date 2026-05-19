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
- [Find text](#find-text) - `str_contains()` and `strpos()` search inside strings
- [Replace text](#replace-text) - `str_replace()` replaces parts of a string
- [Split and join strings](#split-and-join-strings) - `explode()` and `implode()` convert between strings and arrays
- [Convert binary to hex](#convert-binary-to-hex) - `bin2hex()` converts bytes to readable hex text

## Define strings

```php
$name = 'Alice';
$message = "Hello, world";
```

Single quotes create a literal string.
Double quotes allow variable interpolation and escape sequences like `\n`.

## Concatenate strings

```php
$fullName = $firstName . ' ' . $lastName;
```

## Interpolate variables

```php
$message = "Hello, $name";
$title = "User: {$user['name']}";
```

## Access string length

```php
$len = strlen($message);
```

## Trim whitespace

```php
$title = trim($title);
```

## Change case

```php
$upper = strtoupper($name);
$lower = strtolower($name);
```

## Format a string

```php
$text = sprintf('%s has %d messages', $name, $count);
```

## Find text

Use `str_contains()` when you only need a true/false answer.

```php
if (str_contains($email, '@')) {
    echo 'Looks like an email';
}
```

Use `strpos()` when you need the position.

```php
$pos = strpos($filename, '.');

if ($pos !== false) {
    echo 'Extension starts at: ' . $pos;
}
```

## Replace text

```php
$url = str_replace(' ', '-', $title);
```

## Split and join strings

```php
$tags = explode(',', 'php,web,backend');
$line = implode(', ', $tags);
```

## Convert binary to hex

`bin2hex()` is often used to turn random bytes into a readable token.

```php
$hex = bin2hex($bytes);
```
