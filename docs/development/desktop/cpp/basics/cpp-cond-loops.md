# Conditions and loops in C++

[← back](../index.md)

## Summary

- [if / else](#if-else)
- [while](#while)
- [do / while](#do-while)
- [for (classic)](#for-classic)
- [for-each](#for-each)
- [Ternary operator](#ternary-operator)
- [switch](#switch)

## <a id="if-else"></a>if / else

Branch execution based on a condition.

```cpp
if (cond) {
    // code when cond is true
} else {
    // code when cond is false
}
```

## <a id="while"></a>while

Precondition loop: repeats while condition is true.

```cpp
while (cond) {
    // repeated code
}
```

## <a id="do-while"></a>do / while

Postcondition loop: body runs at least one time.

```cpp
do {
    // repeated code
} while (cond);
```

## <a id="for-classic"></a>for (classic)

Loop with init, condition, and step in one line.

```cpp
for (int i = 0; i < n; i++) {
    // repeated code with index i
}
```

## <a id="for-each"></a>for-each

Iterates over array elements directly.

```cpp
for (int x : arr) {
    // work with element x
}
```

## <a id="ternary-operator"></a>Ternary operator

Short form of simple if/else expression.

```cpp
int result = cond ? a : b;
```

## <a id="switch"></a>switch

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
