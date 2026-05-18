# Types in PHP

[← back](../index.md)

## Summary

- [Basic types](#basic-types) - scalar values, exact type names, and helpers like `strlen()`
- [Complex types](#complex-types) - arrays, objects, `null`, and helpers like `count()`
- [Type declarations](#type-declarations) - function parameters, return values, properties, nullable types, unions, and PHPDoc for arrays

## <a id="basic-types"></a>1. Basic types

These are the exact type names used in function parameters, return values, and class properties:

| Value type | Type name in code | Example value |
| --- | --- | --- |
| [Boolean](#boolean) | `bool` | `true`, `false` |
| [Integer](#numbers) | `int` | `255` |
| [Floating point number](#numbers) | `float` | `199.50` |
| [String](#string) | `string` | `'hello'` |
| [Array](#array) | `array` | `[1, 2, 3]` |
| [Object](#object) | class name or `object` | `User`, `object` |
| [No value](#null) | `null` | `null` |

Use these names exactly: `bool`, not `boolean`; `int`, not `integer`; `float`, not `double`.
PHP does not have a separate `char` type. A single character is a `string` with length 1.

### <a id="boolean"></a>Boolean

```php
$b = true;
```

### <a id="numbers"></a>Numbers

Integer numbers
```php
$a = 255;
$b = 15000;
$x = 64000;
$y = 8000000000;
```

Floating point numbers:
```php
$x = 199.50;
$y = 3.14159265359;
```

### <a id="string"></a>String

```php
$hello = "hello world"; // double quotes
$letter = 'A';          // single quotes
```

Access string char by index
```php
$c = $name[5];
```

Get string length
```php
$len = strlen($name);
```

## <a id="complex-types"></a>2. Complex types

### <a id="array"></a>Array

Array can work as a list or as a dictionary.

Define an array with initialization
```php
$arr = [128, 256, 512, 1024];
$user = [
    'name' => 'Alice',
    'age' => 25,
];
```

Access array element by index or key
```php
$x = $arr[2];
$name = $user['name'];
```

Get array length
```php
$len = count($arr);
```

### <a id="object"></a>Object

Object is an instance of a class.

Declare class
```php
class User {
    public string $name;
}
```

Use object
```php
$user = new User();
$user->name = 'Alice';
```

### <a id="null"></a>null

`null` means "no value".

```php
$value = null;
```

## <a id="type-declarations"></a>3. Type declarations

Type declarations make PHP check what values can be passed to a function, returned from a function, or stored in a class property.

### Function parameters

```php
function greet(string $name, bool $loud): string {
    $message = 'Hello, ' . $name;

    if ($loud) {
        return strtoupper($message);
    }

    return $message;
}

echo greet('Alice', true);
```

### Return values

Put the return type after `:`.

```php
function add(int $a, int $b): int {
    return $a + $b;
}

function priceWithTax(float $price): float {
    return $price * 1.2;
}

function getTags(): array {
    return ['php', 'backend'];
}
```

### No return value: `void`

Use `void` when a function performs an action but does not return a value.

```php
function logMessage(string $message): void {
    echo $message;
}
```

### Class properties

```php
class Product {
    public int $id;
    public string $name;
    public float $price;
    public bool $available;
}
```

### Object and class types

Use a class name when the value must be an instance of that class.

```php
class User {
    public string $email;
}

function sendWelcomeEmail(User $user): void {
    echo 'Welcome, ' . $user->email;
}
```

Use `object` only when any object is allowed.

```php
function debugObject(object $value): void {
    var_dump($value);
}
```

### Nullable types

Add `?` before the type name when the value can also be `null`.

```php
function findUserEmail(int $userId): ?string {
    if ($userId === 1) {
        return 'alice@example.com';
    }

    return null;
}
```

This is the same idea as `string|null`, but `?string` is shorter.

### Union types

Use `|` when a value can have one of several types.

```php
function formatId(int|string $id): string {
    return 'ID: ' . $id;
}

function getDiscount(): int|float {
    return 10.5;
}
```

### Array element types

PHP can declare only `array` in the function signature.
Element types are usually written in a PHPDoc comment.

```php
/**
 * @param string[] $names
 * @return int[]
 */
function nameLengths(array $names): array {
    $lengths = [];

    foreach ($names as $name) {
        $lengths[] = strlen($name);
    }

    return $lengths;
}
```

### Common special types

| Type name | Meaning |
| --- | --- |
| `mixed` | Any value is allowed |
| `callable` | A function, closure, or callable method |
| `iterable` | An `array` or object that can be used in `foreach` |
| `never` | The function never returns normally |

Examples:

```php
function dumpValue(mixed $value): void {
    var_dump($value);
}

function apply(callable $callback, int $value): mixed {
    return $callback($value);
}

function printItems(iterable $items): void {
    foreach ($items as $item) {
        echo $item;
    }
}

function stop(string $message): never {
    throw new RuntimeException($message);
}
```

PHP also has a `resource` value type for things like file handles, but `resource` is not used as a normal type declaration.
