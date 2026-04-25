# Arrays in old C/C++

[← back](index.md)

## 1. Idea

Before `std::array` and `std::vector`, arrays were usually fixed-size built-in arrays.

```cpp
int arr[5];
```

Array size is usually fixed after declaration.

## 2. Declare array

```cpp
int arr[5];
char letters[3];
double prices[10];
```

Example with initialization:

```cpp
int nums[5] = { 10, 20, 30, 40, 50 };
```

## 3. Partial initialization

```cpp
int arr[5] = { 1, 2 };
```

Result:
* `arr[0] = 1`
* `arr[1] = 2`
* other elements become `0`

Initialize all with zero:

```cpp
int arr[5] = {};
```

## 4. Size by initializer

Compiler can detect size automatically:

```cpp
int arr[] = { 10, 20, 30, 40 };
```

Here size is `4`.

## 5. Access elements

```cpp
int arr[] = { 10, 20, 30 };

int a = arr[0];
arr[1] = 99;
```

Index starts from `0`.

## 6. Array length

For local built-in arrays:

```cpp
int arr[] = { 10, 20, 30, 40 };
int len = sizeof(arr) / sizeof(arr[0]);
```

This works only when array is still a real array, not a function parameter.

## 7. Loop through array

Classic loop:

```cpp
int arr[] = { 10, 20, 30 };
int len = sizeof(arr) / sizeof(arr[0]);

for (int i = 0; i < len; i++) {
    std::cout << arr[i] << '\n';
}
```

## 8. Multidimensional arrays

```cpp
int table[2][3] = {
    { 1, 2, 3 },
    { 4, 5, 6 }
};
```

Access element:

```cpp
int x = table[1][2];   // 6
```

## 9. Arrays in functions

When passed to a function, array becomes a pointer to the first element.

```cpp
void printArray(int arr[], int len) {
    for (int i = 0; i < len; i++) {
        std::cout << arr[i] << '\n';
    }
}
```

Call:

```cpp
int nums[] = { 5, 10, 15 };
printArray(nums, 3);
```

Because of this, function usually needs array length as a separate argument.

## 10. Copy array

Built-in arrays cannot be assigned directly.

Wrong:

```cpp
int a[3] = { 1, 2, 3 };
int b[3];

b = a;   // wrong
```

Copy with loop:

```cpp
for (int i = 0; i < 3; i++) {
    b[i] = a[i];
}
```

## 11. Limitations

Old built-in arrays:
* have fixed size
* do not know their own length in function parameters
* cannot be assigned directly
* do not resize automatically
* can easily go out of bounds

For modern C++ code, `std::array` and `std::vector` are usually more convenient and safer.
