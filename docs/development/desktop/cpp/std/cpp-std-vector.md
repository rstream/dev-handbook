# std::vector in C++

[← back](../index.md)

Use `std::vector` when you need an array that can grow or shrink while the program runs.
It is the usual replacement for manual dynamic arrays in modern C++.

## Summary

- [Include header](#include-header) - use `#include <vector>`
- [Declare vector](#declare-vector) - create empty vectors and vectors with values
- [Add elements](#add-elements) - append values with `push_back()`
- [Access elements](#access-elements) - read and change values by index
- [Size](#size) - get element count with `size()`
- [Loop through vector](#loop-through-vector) - use range-based `for`
- [Remove elements](#remove-elements) - remove from the end with `pop_back()`
- [Clear vector](#clear-vector) - remove all elements with `clear()`
- [Pass to function](#pass-to-function) - pass by reference to avoid copying

## <a id="include-header"></a>Include header

`std::vector` is declared in `<vector>`.

```cpp
#include <vector>
```

For input and output you usually also need `<iostream>`.

```cpp
#include <iostream>
#include <vector>
```

## <a id="declare-vector"></a>Declare vector

Create an empty vector:

```cpp
std::vector<int> numbers;
```

Create a vector with values:

```cpp
std::vector<int> values = { 10, 20, 30 };
```

Create a vector with a fixed initial size:

```cpp
std::vector<int> values(5);       // 5 elements with value 0
std::vector<int> scores(5, 100);  // 5 elements with value 100
```

## <a id="add-elements"></a>Add elements

Use `push_back()` to append a value to the end.

```cpp
std::vector<int> numbers;

numbers.push_back(10);
numbers.push_back(20);
numbers.push_back(30);
```

The vector grows automatically.

## <a id="access-elements"></a>Access elements

Index starts from `0`.

```cpp
std::vector<int> values = { 10, 20, 30 };

int first = values[0];   // 10
values[1] = 99;
```

Use `front()` and `back()` for first and last elements.

```cpp
int a = values.front();
int b = values.back();
```

Be careful with empty vectors.
`front()` and `back()` require at least one element.

## <a id="size"></a>Size

Use `size()` to get the number of elements.

```cpp
std::vector<int> values = { 10, 20, 30 };

int len = values.size();   // 3
```

Check if a vector is empty:

```cpp
if (values.empty()) {
    std::cout << "no values\n";
}
```

## <a id="loop-through-vector"></a>Loop through vector

Use a range-based `for` loop to read values.

```cpp
std::vector<int> values = { 10, 20, 30 };

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

## <a id="remove-elements"></a>Remove elements

Use `pop_back()` to remove the last element.

```cpp
std::vector<int> values = { 10, 20, 30 };

values.pop_back();
```

After this, `values` contains `10` and `20`.
Call `pop_back()` only when the vector is not empty.

## <a id="clear-vector"></a>Clear vector

Use `clear()` to remove all elements.

```cpp
std::vector<int> values = { 10, 20, 30 };

values.clear();
```

After `clear()`, `values.size()` is `0`.

## <a id="pass-to-function"></a>Pass to function

Use `const std::vector<int>&` when a function only reads the vector.

```cpp
void printVector(const std::vector<int>& values) {
    for (int value : values) {
        std::cout << value << '\n';
    }
}
```

Use `std::vector<int>&` when a function should change the vector.

```cpp
void addDefaultValue(std::vector<int>& values) {
    values.push_back(0);
}
```
