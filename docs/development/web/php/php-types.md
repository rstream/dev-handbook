# Types in PHP

[← back](./index.md)

## 1. Basic types

### Boolean

```php
$b = true;
```

### Numbers

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

### String

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

## 2. Complex types

### Array

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

### Object

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

### null

`null` means "no value".

```php
$value = null;
```
