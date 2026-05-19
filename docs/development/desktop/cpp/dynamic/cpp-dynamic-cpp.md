# Dynamic memory in C++

[← back](../index.md)

## Summary

- [Idea](#idea)
- [Allocate one object](#allocate-one-object)
- [Allocate with initialization](#allocate-with-initialization)
- [Allocate array](#allocate-array)
- [Objects and constructors](#objects-and-constructors)
- [Common mistakes](#common-mistakes)
- [new vs malloc](#new-vs-malloc)
- [Modern C++ recommendation](#modern-cpp-recommendation)

## <a id="idea"></a>1. Idea

In C++, dynamic memory is commonly allocated with:
* `new`
* `delete`
* `new[]`
* `delete[]`

Unlike `malloc`, `new` creates objects and calls constructors.

## <a id="allocate-one-object"></a>2. Allocate one object

```cpp
int* ptr = new int;
*ptr = 42;
```

Release memory:

```cpp
delete ptr;
ptr = nullptr;
```

## <a id="allocate-with-initialization"></a>3. Allocate with initialization

```cpp
int* a = new int(25);
double* b = new double(3.14);
```

Example:

```cpp
std::cout << *a << '\n';
```

## <a id="allocate-array"></a>4. Allocate array

```cpp
int* arr = new int[5];
```

Fill values:

```cpp
for (int i = 0; i < 5; i++) {
    arr[i] = i * 100;
}
```

Release array:

```cpp
delete[] arr;
arr = nullptr;
```

Use `delete[]` only for memory created with `new[]`.

## <a id="objects-and-constructors"></a>5. Objects and constructors

For class objects, `new` calls constructor and `delete` calls destructor.

```cpp
class User {
public:
    std::string name;

    User() {
        name = "Guest";
    }
};

User* user = new User();
delete user;
```

This is one important difference from `malloc/free`.

## <a id="common-mistakes"></a>6. Common mistakes

Wrong:

```cpp
int* arr = new int[5];
delete arr;      // wrong
```

Correct:

```cpp
int* arr = new int[5];
delete[] arr;    // correct
```

Also wrong:

* forgetting `delete`
* using pointer after `delete`
* deleting the same pointer twice

## <a id="new-vs-malloc"></a>7. `new` vs `malloc`

`new`
* returns correct pointer type
* calls constructors
* works naturally with C++ objects

`malloc`
* allocates raw memory
* returns `void*`
* does not call constructors

For normal C++ code, `new/delete` are better than `malloc/free`.

## <a id="modern-cpp-recommendation"></a>8. Modern C++ recommendation

Even `new/delete` are not the best default choice in modern C++.

Usually it is better to use:
* `std::vector` instead of dynamic arrays
* `std::string` instead of manual char buffers
* `std::unique_ptr` or `std::shared_ptr` instead of manual `new/delete`

Example:

```cpp
#include <memory>

std::unique_ptr<int> ptr = std::make_unique<int>(42);
```

Memory will be released automatically.

## <a id="summary-2"></a>9. Summary

* use `new` for one object
* use `new[]` for arrays
* use `delete` for memory from `new`
* use `delete[]` for memory from `new[]`
* prefer containers and smart pointers in modern C++ code
