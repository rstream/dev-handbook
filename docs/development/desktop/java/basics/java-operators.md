# Operators in Java

[← back](../index.md)

Operators are symbols that perform operations on values and variables.

## Summary

- [Arithmetic](#arithmetic) - numeric operations
- [Assignment](#assignment) - assign and update values
- [Comparison](#comparison) - compare values
- [Logical](#logical) - combine boolean expressions
- [Increment and decrement](#increment-and-decrement) - add or subtract one
- [Bitwise](#bitwise) - work with integer bits
- [Shift](#shift) - move bits left or right
- [instanceof](#instanceof) - check object type
- [Operator precedence](#operator-precedence) - expression evaluation order

## Arithmetic
Used with numeric values.

```java
int a = 10;
int b = 3;

int sum = a + b;        // 13
int diff = a - b;       // 7
int product = a * b;    // 30
int quotient = a / b;   // 3, integer division
int remainder = a % b;  // 1
```

With floating point numbers, division keeps the fractional part.

```java
double x = 10.0 / 3.0; // 3.3333333333333335
```

## Assignment
Assigns values to variables.

```java
int x = 10;

x += 5;  // x = x + 5
x -= 2;  // x = x - 2
x *= 3;  // x = x * 3
x /= 4;  // x = x / 4
x %= 2;  // x = x % 2
```

## Comparison
Comparison operators return `boolean`.

```java
int a = 10;
int b = 20;

boolean eq = a == b;  // false
boolean ne = a != b;  // true
boolean lt = a < b;   // true
boolean le = a <= b;  // true
boolean gt = a > b;   // false
boolean ge = a >= b;  // false
```

Use `.equals()` to compare object contents, for example strings.

```java
String a = "hello";
String b = "hello";

boolean sameText = a.equals(b); // true
```

## Logical
Used with `boolean` values.

```java
boolean a = true;
boolean b = false;

boolean and = a && b; // false
boolean or = a || b;  // true
boolean not = !a;     // false
```

`&&` and `||` use short-circuit evaluation: Java does not evaluate the right side when the result is already known.

```java
if (name != null && name.length() > 0) {
    System.out.println(name);
}
```

## Increment and decrement
```java
int x = 5;

x++; // x = x + 1
x--; // x = x - 1
```

Prefix changes the value before using it. Postfix changes the value after using it.

```java
int a = 5;
int b = ++a; // a = 6, b = 6

int x = 5;
int y = x++; // x = 6, y = 5
```

## Bitwise
Used with integer values.

```java
int a = 0b1100;
int b = 0b1010;

int and = a & b;  // 0b1000
int or = a | b;   // 0b1110
int xor = a ^ b;  // 0b0110
int not = ~a;     // inverted bits
```

## Shift
Moves bits left or right.

```java
int x = 8;       // 0b01000

int left = x << 1;          // 16 (0b10000)
int right = x >> 1;         // 4  (0b00100)
int unsignedRight = x >>> 1;
```

* `>>` keeps the sign bit.
* `>>>` fills left bits with zeros.

## instanceof
Checks whether an object has a specific type.

```java
Object value = "hello";

if (value instanceof String) {
    System.out.println("value is string");
}
```

Check the type and create a copy of var with a strict type:

```java
Object value = "hello";

if (value instanceof String value_text) {
    System.out.println(value_text.length());
}
```

Longer version:

```java
Object value = "hello";

if (value instanceof String) {
    String value_text = (String)value;
    System.out.println(value_text.length());
}
```

## Operator precedence
Operators with higher precedence run first. Use parentheses when the expression is not obvious.

```java
int x = 2 + 3 * 4;   // 14
int y = (2 + 3) * 4; // 20
```
