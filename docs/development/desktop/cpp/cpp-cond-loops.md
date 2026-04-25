# Conditions and loops in C++

[← back](index.md)

## if / else

Branch execution based on a condition.

```cpp
if (cond) {
    // code when cond is true
} else {
    // code when cond is false
}
```

## while

Precondition loop: repeats while condition is true.

```cpp
while (cond) {
    // repeated code
}
```

## do / while

Postcondition loop: body runs at least one time.

```cpp
do {
    // repeated code
} while (cond);
```

## for (classic)

Loop with init, condition, and step in one line.

```cpp
for (int i = 0; i < n; i++) {
    // repeated code with index i
}
```

## for-each

Iterates over array elements directly.

```cpp
for (int x : arr) {
    // work with element x
}
```

## Ternary operator

Short form of simple if/else expression.

```cpp
int result = cond ? a : b;
```

## switch

Multiple branches by value with `case`, `break`, and optional `default`.

```cpp
switch (x) {
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
