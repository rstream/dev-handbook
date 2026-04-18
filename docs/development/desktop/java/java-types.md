# Types in Java

[← back](index.md)

## 1. Basic types

### Boolean

```java
bool b = true; // 1 byte
```

### Numbers

Integer numbers
```java
byte a = 255;        // 8 bit
short b = 15000;     // 16 bit 
int x = 64000;       // 32 bit
long y = 8000000000; // 64 bit
```

Floating point numbers:
```java
float x = 199.50;              // 32 bit
double y = 3.14159265359; // 64 bit
```

### Char

```java
char c = 'A'; // 16 bit; single quotes!
```

## 2. Complex types

### String

String is a class.  

```java
String hello = "hello world"; // double quotes
String dragons = new String("green dragons");
```

Access string char by index
```java
char c = name.charAt(5);
```

Get string length
```java
int len = name.length(); // not method
```

### Array

Array is a class with a fixed size.

Define an array with defined size (all elements are zeros)
```java
int[] arr = new int[10];        // single dimension
int[][] table = new int[3][10]; // 3 rows, 10 columns 
```

Define an array with initialization
```java
int[] arr = { 128, 256, 512, 1024 };
int[][] table {
	{ 128, 256, 512 },
	{ 1024, 2048, 4096 }
}; 
```

Access array element by index
```java
int x = arr[5];
```

Get array length
```java
int len = arr.length; // field, not method
```

### enum

Declare enum
```java
enum Color { RED, GREEN, BLUE };
```

Use enum
```java
COLOR c = Color.RED;
```