# Arrays in PHP

[← back](../index.md)

An array can work as a list of values or as a dictionary with named keys.

## Summary

- [Indexed array](#indexed-array) - list-like arrays
- [Associative array](#associative-array) - dictionary-like arrays with named keys
- [Add elements](#add-elements) - append values and assign keys
- [Get array length](#get-array-length) - `count()` counts elements
- [Loop through an array](#loop-through-an-array) - iterate with `foreach`
- [Check that a key exists](#check-that-a-key-exists) - `array_key_exists()` tests for a key
- [Use a fallback value](#use-a-fallback-value) - default value with `??`

## <a id="indexed-array"></a>Indexed array

```php
$colors = ['red', 'green', 'blue'];
```

Access by index:

```php
$first = $colors[0];
```

## <a id="associative-array"></a>Associative array

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

## <a id="add-elements"></a>Add elements

```php
$colors[] = 'black';
$user['role'] = 'admin';
```

## <a id="get-array-length"></a>Get array length

```php
$count = count($colors);
```

## <a id="loop-through-an-array"></a>Loop through an array

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

## <a id="check-that-a-key-exists"></a>Check that a key exists

```php
$hasEmail = array_key_exists('email', $user);
```

## <a id="use-a-fallback-value"></a>Use a fallback value

```php
$theme = $settings['theme'] ?? 'default';
```
