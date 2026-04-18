# Conditions and loops in Java

[← back](index.md)

## if / else

Branch execution based on a condition.

```java
if (cond) {
    // code when cond is true
} else {
    // code when cond is false
}
```

## while

Precondition loop: repeats while condition is true.

```java
while (cond) {
    // repeated code
}
```

## do / while

Postcondition loop: body runs at least one time.

```java
do {
    // repeated code
} while (cond);
```

## for (classic)

Loop with init, condition, and step in one line.

```java
for (int i = 0; i < n; i++) {
    // repeated code with index i
}
```

## for-each

Iterates over array elements directly.

```java
for (int x : arr) {
    // work with element x
}
```

## Ternary operator

Short form of simple if/else expression.

```java
int result = (cond) ? a : b;
```

## switch

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
