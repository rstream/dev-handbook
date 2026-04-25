# Types in C++

[← back](index.md)

## 1. Basic types

### Boolean

```cpp
bool b = true; // usually 1 byte
```

### Numbers

Integer numbers
```cpp
short a = 32000;              // at least 16 bit
int b = 64000;                // usually 32 bit
long c = 1000000L;            // 32 or 64 bit
long long d = 8000000000LL;   // at least 64 bit
unsigned int e = 255;         // unsigned integer
```

Floating point numbers:
```cpp
float x = 199.50f;            // 32 bit
double y = 3.14159265359;     // 64 bit
long double z = 3.14159265359L; // extended precision
```

### Char

```cpp
char c = 'A'; // single quotes
```

## 2. Complex types

### String

String can be defined as an array of chars with a fixed size.

```cpp
char hello[] = "hello";              // array size is 6 with '\0'
char name[20] = "John";              // fixed size array
```

Access string char by index
```cpp
char c = name[5];
```

Get string length
```cpp
#include <cstring>

int len = strlen(name);
```

### Array

Array has a fixed size.

Define an array with defined size
```cpp
int arr[10] = {};         // all elements are zeros
int table[3][10] = {};    // 3 rows, 10 columns
```

Define an array with initialization
```cpp
int arr[] = { 128, 256, 512, 1024 };
int table[2][3] = {
    { 128, 256, 512 },
    { 1024, 2048, 4096 }
};
```

Access array element by index
```cpp
int x = arr[2];
```

Get array length
```cpp
int len = sizeof(arr) / sizeof(arr[0]);
```

### enum

Declare enum
```cpp
enum Color { RED, GREEN, BLUE };
```

Use enum
```cpp
Color c = RED;
```
