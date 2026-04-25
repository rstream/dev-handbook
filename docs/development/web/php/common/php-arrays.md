# Arrays in PHP

[← back](../index.md)

An array can work as a list of values or as a dictionary with named keys.

## Indexed array

```php
$colors = ['red', 'green', 'blue'];
```

Access by index:

```php
$first = $colors[0];
```

## Associative array

```php
$user = [
    'name' => 'Alice',
    'email' => 'alice@example.com',
];
```

Access by key:

```php
$name = $user['name'];
```

## Add elements

```php
$colors[] = 'black';
$user['role'] = 'admin';
```

## Get array length

```php
$count = count($colors);
```

## Loop through an array

```php
foreach ($colors as $color) {
    echo $color;
}
```

```php
foreach ($user as $key => $value) {
    echo $key . ': ' . $value;
}
```

## Check that a key exists

```php
$hasEmail = array_key_exists('email', $user);
```

## Use a fallback value

```php
$theme = $settings['theme'] ?? 'default';
```
