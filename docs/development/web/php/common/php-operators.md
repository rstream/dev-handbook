# Operators in PHP

[← back](../index.md)

## 1. Arithmetic operators

```php
$a + $b; // addition
$a - $b; // subtraction
$a * $b; // multiplication
$a / $b; // division
$a % $b; // remainder
```

Numeric strings are converted to numbers in arithmetic expressions:
```php
$x = "10" + 5; // 15
```

## 2. Assignment operators

```php
$x = 10;
$x += 5; // same as: $x = $x + 5
$x -= 2;
$x *= 3;
$x /= 4;
```

## 3. String operator

Use `.` to concatenate strings.

```php
$firstName = 'John';
$lastName = 'Smith';

$fullName = $firstName . ' ' . $lastName;
```

## 4. Comparison operators

### Loose comparison: `==`

`==` compares values after implicit type conversion.

```php
var_dump(5 == "5");     // true
var_dump(0 == false);   // true
var_dump("" == false);  // true
```

This can be convenient, but it can also hide bugs.

### Strict comparison: `===`

`===` compares both value and type.

```php
var_dump(5 === "5");    // false
var_dump(5 === 5);      // true
var_dump(0 === false);  // false
```

Use `===` when you need predictable comparison without implicit type conversion.

### Not equal

```php
$a != $b;  // loose: values are different after type conversion
$a !== $b; // strict: values or types are different
```

## 5. Relational operators

```php
$a > $b;
$a < $b;
$a >= $b;
$a <= $b;
```

## 6. Logical operators

```php
$a && $b; // and
$a || $b; // or
!$a;      // not
```

Example:
```php
if ($age >= 18 && $isActive) {
    echo 'Access allowed';
}
```

## 7. Null coalescing operator

`??` returns the left value if it exists and is not `null`, otherwise it returns the right value.

```php
$name = $_GET['name'] ?? 'Guest';
```

This is useful for optional request parameters and default values.
