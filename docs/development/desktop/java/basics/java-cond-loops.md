# Conditions and loops in Java

[← back](../index.md)

## Summary

- [if / else](#if-else) - branch execution by condition
- [while](#while) - precondition loop
- [do / while](#do-while) - postcondition loop
- [for classic](#for-classic) - loop with init, condition, and step
- [for-each](#for-each) - iterate over array elements
- [Ternary operator](#ternary-operator) - short conditional expression
- [switch](#switch) - multiple branches by value

## <a id="if-else"></a>if / else

Branch execution based on a condition.

```java
if (cond) {
    // code when cond is true
} else {
    // code when cond is false
}
```

## <a id="while"></a>while

Precondition loop: repeats while condition is true.

```java
while (cond) {
    // repeated code
}
```

## <a id="do-while"></a>do / while

Postcondition loop: body runs at least one time.

```java
do {
    // repeated code
} while (cond);
```

## <a id="for-classic"></a>for (classic)

Loop with init, condition, and step in one line.

```java
for (int i = 0; i < n; i++) {
    // repeated code with index i
}
```

## <a id="for-each"></a>for-each

Iterates over array elements directly.

```java
for (int x : arr) {
    // work with element x
}
```

## <a id="ternary-operator"></a>Ternary operator

Short form of simple if/else expression.

```java
int result = cond ? a : b;
```

## <a id="switch"></a>switch

### classic syntax
Multiple branches by value with `case`, `break`, and optional `default`.

```java
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

### new syntax

Arrow form (`->`) without fall-through. Can also be used as expression.

```java
String text = switch (x) {
    case 1 -> "one";
    case 2 -> "two";
    default -> "other";
};
```

```java
int value = switch (x) {
    case 1 -> {
        int y = 10;
        yield y + 1;
    }
    default -> 0;
};
```
* `yield` returns a value and used when there are several lines of code in the **case** block.
