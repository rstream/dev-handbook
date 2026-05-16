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
- [Check that a value exists](#check-that-a-value-exists) - `in_array()` tests for a value
- [Use a fallback value](#use-a-fallback-value) - default value with `??`
- [Filter array values](#filter-array-values) - `array_filter()` keeps matching items
- [Transform array values](#transform-array-values) - `array_map()` builds a changed array
- [Reset numeric indexes](#reset-numeric-indexes) - `array_values()` reindexes list-like arrays

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

## <a id="check-that-a-value-exists"></a>Check that a value exists

Use strict mode (`true`) when types should match too.

```php
$allowed = ['admin', 'editor', 'viewer'];

if (in_array($role, $allowed, true)) {
    echo 'Role is allowed';
}
```

## <a id="use-a-fallback-value"></a>Use a fallback value

```php
$theme = $settings['theme'] ?? 'default';
```

## <a id="filter-array-values"></a>Filter array values

```php
$activeUsers = array_filter($users, function (array $user): bool {
    return $user['active'];
});
```

## <a id="transform-array-values"></a>Transform array values

```php
$names = array_map(function (array $user): string {
    return $user['name'];
}, $users);
```

## <a id="reset-numeric-indexes"></a>Reset numeric indexes

`array_filter()` keeps the original keys.
Use `array_values()` when you need a clean list with numeric indexes from `0`.

```php
$activeUsers = array_values($activeUsers);
```
