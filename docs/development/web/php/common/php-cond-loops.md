# Conditions and loops in PHP

[← back](../index.md)

## if / else

Branch execution based on a condition.

```php
if ($cond) {
    // code when $cond is true
} else {
    // code when $cond is false
}
```

## while

Precondition loop: repeats while condition is true.

```php
while ($cond) {
    // repeated code
}
```

## do / while

Postcondition loop: body runs at least one time.

```php
do {
    // repeated code
} while ($cond);
```

## for (classic)

Loop with init, condition, and step in one line.

```php
for ($i = 0; $i < $n; $i++) {
    // repeated code with index $i
}
```

## foreach

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

## Ternary operator

Short form of simple if/else expression.

```php
$result = $cond ? $a : $b;
```

## switch

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

## match

Expression form for choosing a value without fall-through.

```php
$text = match ($x) {
    1 => 'one',
    2 => 'two',
    default => 'other',
};
```
