# Function pointers and callbacks in C++

[← back](index.md)

## 1. Function pointer

A function pointer stores the address of a function.

```cpp
int sum(int a, int b) {
    return a + b;
}

int (*op)(int, int) = sum;
```

The pointer type must match the function signature.

## 2. Call through function pointer

```cpp
int result1 = op(2, 3);
int result2 = (*op)(2, 3);
```

Both calls are valid.

## 3. Another example

```cpp
void hello() {
    std::cout << "Hello\n";
}

void (*printer)() = hello;
printer();
```

## 4. `typedef` and `using`

Function pointer syntax can be hard to read, so aliases are often used.

With `typedef`:

```cpp
typedef int (*Operation)(int, int);
```

With `using`:

```cpp
using Operation = int (*)(int, int);
```

Example:

```cpp
int mul(int a, int b) {
    return a * b;
}

Operation op = mul;
int result = op(4, 5);
```

## 5. Callback idea

A callback is a function passed to another function, so it can be called later.

```cpp
void run(Operation op, int a, int b) {
    int result = op(a, b);
    std::cout << result << '\n';
}
```

Use callback:

```cpp
int sum(int a, int b) {
    return a + b;
}

int sub(int a, int b) {
    return a - b;
}

run(sum, 10, 5); // 15
run(sub, 10, 5); // 5
```

## 6. Callback for processing values

```cpp
void process(int* arr, int len, void (*handler)(int)) {
    for (int i = 0; i < len; i++) {
        handler(arr[i]);
    }
}

void printNumber(int x) {
    std::cout << x << '\n';
}
```

Use:

```cpp
int arr[] = { 3, 6, 9 };
process(arr, 3, printNumber);
```

## 7. Why callbacks are useful

Callbacks help when:
* different behavior must be selected dynamically
* one function should reuse external logic
* event-based systems call user code later

## 8. Notes

* function pointers can point only to regular functions with matching signature
* member functions have different syntax and cannot be used the same way directly
* in modern C++, callbacks are often implemented with lambdas and `std::function`, but function pointers are still useful for simple cases
