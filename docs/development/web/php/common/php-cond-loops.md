# Conditions and loops in PHP

[← back](../index.md)

## Summary

- [if / else](#if-else) - choose between branches by condition
- [while](#while) - repeat while condition is true
- [do / while](#do-while) - run the body at least once
- [for](#for) - classic counted loop
- [foreach](#foreach) - iterate over array values or key/value pairs
- [Ternary operator](#ternary-operator) - short conditional expression
- [switch](#switch) - multiple branches by value
- [match](#match) - expression form for choosing a value

## <a id="if-else"></a>if / else

Branch execution based on a condition.

```php
if ($cond) {
    // code when $cond is true
} else {
    // code when $cond is false
}
```

## <a id="while"></a>while

Precondition loop: repeats while condition is true.

```php
while ($cond) {
    // repeated code
}
```

## <a id="do-while"></a>do / while

Postcondition loop: body runs at least one time.

```php
do {
    // repeated code
} while ($cond);
```

## <a id="for"></a>for (classic)

Loop with init, condition, and step in one line.

```php
for ($i = 0; $i < $n; $i++) {
    // repeated code with index $i
}
```

## <a id="foreach"></a>foreach

Iterates over array elements directly.

```php
foreach ($arr as $value) {
    // work with element $value
}
```

```php
foreach ($arr as $key => $value) {
    // work with key and value
}
```

## <a id="ternary-operator"></a>Ternary operator

Short form of simple if/else expression.

```php
$result = $cond ? $a : $b;
```

## <a id="switch"></a>switch

Multiple branches by value with `case`, `break`, and optional `default`.

```php
switch ($x) {
    case 1:
        // code for 1
        break;
    case 2:
        // code for 2
        break;
    default:
        // fallback code
}
```

## <a id="match"></a>match

Expression form for choosing a value without fall-through.

```php
$text = match ($x) {
    1 => 'one',
    2 => 'two',
    default => 'other',
};
```
