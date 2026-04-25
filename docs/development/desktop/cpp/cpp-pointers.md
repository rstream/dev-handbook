# Pointers in C++

[← back](index.md)

## 1. What is a pointer

A pointer stores a memory address of another object.

```cpp
int value = 10;
int* ptr = &value;
```

Where:
* `value` - normal integer variable
* `&value` - address of variable `value`
* `ptr` - pointer to `int`

## 2. Declare a pointer

```cpp
int* a;
char* text;
double* price;
```

Pointer type must match the type of the object it points to.

## 3. Get address

Use operator `&` to get an address:

```cpp
int value = 25;
int* ptr = &value;
```

## 4. Dereference pointer

Use operator `*` to access the value by address:

```cpp
int value = 25;
int* ptr = &value;

int x = *ptr;   // x = 25
*ptr = 99;      // value becomes 99
```

## 5. Null pointer

A pointer can point to nothing:

```cpp
int* ptr = nullptr;
```

Always check such pointers before dereferencing:

```cpp
if (ptr != nullptr) {
    std::cout << *ptr << '\n';
}
```

## 6. Pointers and arrays

Array name can be used as a pointer to the first element.

```cpp
int arr[] = { 10, 20, 30 };
int* ptr = arr;

int a = ptr[0];
int b = *(ptr + 1);
```

## 7. Pointer arithmetic

For arrays, pointer can move between elements:

```cpp
int arr[] = { 10, 20, 30 };
int* ptr = arr;

ptr = ptr + 1;    // now points to arr[1]
int x = *ptr;     // 20
```

Pointer arithmetic depends on pointed type size.

## 8. Pass by pointer

Pointers are often used to modify variables inside a function.

```cpp
void setZero(int* value) {
    *value = 0;
}

int main() {
    int x = 15;
    setZero(&x);
}
```

After call, `x` becomes `0`.

## 9. Pointer to pointer

Pointer can also store address of another pointer.

```cpp
int value = 7;
int* ptr = &value;
int** ptr2 = &ptr;
```

Access value:

```cpp
int x = **ptr2;
```

## 10. Important notes

* uninitialized pointers are dangerous
* `nullptr` is safer than old `NULL`
* do not dereference invalid or null pointers
* for dynamic memory in modern C++, smart pointers are usually preferred over raw pointers
