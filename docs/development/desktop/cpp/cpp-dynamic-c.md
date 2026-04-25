# Dynamic memory in C style

[← back](index.md)

## 1. Idea

Dynamic memory is memory allocated during program execution, not at compile time.

In C style, dynamic memory is usually managed with:
* `malloc`
* `calloc`
* `realloc`
* `free`

These functions are declared in:

```cpp
#include <cstdlib>
```

## 2. `malloc`

`malloc` allocates a block of memory of given size in bytes.

```cpp
int* ptr = (int*)malloc(sizeof(int));
```

Example:

```cpp
#include <cstdlib>

int main() {
    int* ptr = (int*)malloc(sizeof(int));
    *ptr = 25;

    free(ptr);
}
```

`malloc` does not initialize the memory.

## 3. Allocate array

```cpp
int* arr = (int*)malloc(5 * sizeof(int));
```

Use allocated memory like a normal array:

```cpp
for (int i = 0; i < 5; i++) {
    arr[i] = i * 10;
}
```

After usage:

```cpp
free(arr);
```

## 4. `calloc`

`calloc` allocates memory for multiple elements and initializes all bytes to zero.

```cpp
int* arr = (int*)calloc(5, sizeof(int));
```

Example:

```cpp
for (int i = 0; i < 5; i++) {
    std::cout << arr[i] << '\n';
}
```

All elements are initially zero.

## 5. `realloc`

`realloc` changes the size of an already allocated memory block.

```cpp
int* arr = (int*)malloc(3 * sizeof(int));
arr = (int*)realloc(arr, 6 * sizeof(int));
```

After `realloc`, pointer value may change, because memory can be moved to another place.

## 6. `free`

Memory allocated by `malloc`, `calloc`, or `realloc` must be released with `free`.

```cpp
free(arr);
arr = nullptr;
```

Setting pointer to `nullptr` after `free` helps avoid accidental use of invalid memory.

## 7. Important limitations

`malloc` and related functions:
* do not call constructors
* do not call destructors
* work with raw memory only
* are usually not recommended for normal C++ objects

Example problem:

```cpp
struct User {
    std::string name;
};

User* user = (User*)malloc(sizeof(User)); // bad idea in C++
```

This is wrong for normal C++ objects, because constructor of `std::string` is not called.

## 8. When to use

In C++ code, C-style dynamic memory is usually used only:
* when working with old C libraries
* when working with raw buffers
* in low-level code with special requirements

For normal C++ development, `new/delete`, containers, or smart pointers are preferred.
