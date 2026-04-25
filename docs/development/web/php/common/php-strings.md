# Strings in PHP

[← back](../index.md)

Strings store text data.
Use them for plain text, formatted messages, paths, HTML fragments, and other text values.

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
