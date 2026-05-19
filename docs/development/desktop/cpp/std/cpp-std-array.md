# std::array in C++

[← back](../index.md)

Use `std::array` when the number of elements is fixed and known at compile time.
It is similar to a built-in array, but it has useful member functions like `size()`.

## Summary

- [Include header](#include-header) - use `#include <array>`
- [Declare array](#declare-array) - create a fixed-size array
- [Access elements](#access-elements) - read and change values by index
- [Size](#size) - get element count with `size()`
- [Loop through array](#loop-through-array) - use range-based `for`
- [Fill values](#fill-values) - set all elements with `fill()`
- [Copy and assign](#copy-and-assign) - copy arrays with `=`
- [Pass to function](#pass-to-function) - keep size information in parameters

## Include header

`std::array` is declared in `<array>`.

```cpp
#include <array>
```

For input and output you usually also need `<iostream>`.

```cpp
#include <array>
#include <iostream>
```

## Declare array

Size is part of the type.

```cpp
std::array<int, 5> numbers;
std::array<int, 3> values = { 10, 20, 30 };
```

Initialize all elements with zero:

```cpp
std::array<int, 5> numbers = {};
```

## Access elements

Index starts from `0`.

```cpp
std::array<int, 3> values = { 10, 20, 30 };

int first = values[0];   // 10
values[1] = 99;
```

Use `front()` and `back()` for first and last elements.

```cpp
int a = values.front();
int b = values.back();
```

## Size

Use `size()` to get the number of elements.

```cpp
std::array<int, 3> values = { 10, 20, 30 };

int len = values.size();   // 3
```

Unlike a built-in array passed to a function, `std::array` keeps its size information.

## Loop through array

Use a range-based `for` loop to read values.

```cpp
std::array<int, 3> values = { 10, 20, 30 };

for (int value : values) {
    std::cout << value << '\n';
}
```

Use a reference when you want to change elements.

```cpp
for (int& value : values) {
    value *= 2;
}
```

## Fill values

Use `fill()` to set all elements to the same value.

```cpp
std::array<int, 5> values;
values.fill(0);
```

## Copy and assign

`std::array` can be copied and assigned directly.

```cpp
std::array<int, 3> a = { 1, 2, 3 };
std::array<int, 3> b;

b = a;
```

This is different from built-in arrays.

## Pass to function

The size is part of the parameter type.

```cpp
void printArray(const std::array<int, 3>& values) {
    for (int value : values) {
        std::cout << value << '\n';
    }
}
```

Use `const std::array<int, 3>&` when the function should read the array without copying it.
