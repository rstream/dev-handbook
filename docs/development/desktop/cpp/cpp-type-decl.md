# Type declarations in C++

[← back](index.md)

## 1. `typedef`

`typedef` creates an alias for an existing type.

```cpp
typedef unsigned long ulong;
typedef int Number;
```

Use alias like a normal type:

```cpp
ulong fileSize = 1024;
Number count = 10;
```

`typedef` is also often used for pointers, arrays, and function types:

```cpp
typedef int* IntPtr;
typedef char Name[32];
typedef int (*Operation)(int, int); // function pointer
```

Example:

```cpp
int sum(int a, int b) {
    return a + b;
}

Operation op = sum;
IntPtr ptr = nullptr;
```

## 2. `using`

`using` is the modern way to declare a type alias. It is clearer and easier to read than `typedef`.

```cpp
using ULong = unsigned long;
using Number = int;
```

Use alias like a normal type:

```cpp
ULong fileSize = 1024;
Number count = 10;
```

It is especially convenient for complex declarations:

```cpp
using IntPtr = int*;
using Name = char[32];
using Operation = int (*)(int, int); // function pointer
```

## 3. Templates with `using`

`using` supports alias templates, which `typedef` cannot do directly.

```cpp
#include <vector>
#include <string>

template <typename T>
using List = std::vector<T>;

List<int> numbers = { 1, 2, 3 };
List<std::string> names = { "Ann", "Bob" };
```

## 4. `typedef` vs `using`

`typedef`
* old C/C++ style
* works well for simple aliases
* harder to read for function pointers and complex types
* does not support alias templates directly

`using`
* modern C++ style
* easier to read
* better for complex types
* supports alias templates

For new C++ code, `using` is recommended in most cases.
