# Console output in Java

[← back](../index.md)

## Summary

- [print](#print) - write text without a new line
- [println](#println) - write text with a new line
- [printf](#printf) - formatted output

## print
Writes text to console without a new line.

```java
System.out.print("Hello");
System.out.print(" World");
```

## println
Writes text and moves cursor to the next line.

```java
System.out.println("Hello");
System.out.println("World");
```

## printf
Formatted output using format specifiers.
* %s - string
* %d - decimal
* %f - float
* %n - next line (OS independent: `\n` for Linux/Mac, `\r\n` for Windows)

```java
String name = "Ann";
int age = 23;
double score = 95.55;

System.out.printf("Name: %s, age: %d, score: %f%n", name, age, score); // "Name: Ann, age: 23, score: 95.55\n" 
```

More float formatting examples:

```java
double score = 95.5;

System.out.printf("Score: %+f%n", score);    // "+95.6" (always show sign)
System.out.printf("Score: %.1f%n", score);   // "95.6" (rounded!)
System.out.printf("Score: %5.1f%n", score);  // "   95.6" (with leading spaces)
System.out.printf("Score: %-5.1f%n", score); // "95.6   " (with spaces after)
System.out.printf("Score: %05.1f%n", score); // "00095.6" (with leading zeros)
```
