# Strings in old C/C++

[← back](index.md)

## 1. Idea

Before `std::string`, strings in C and old C++ were usually stored as arrays of `char`.

```cpp
char text[] = "hello";
```

Such string always ends with special character `'\0'`.

For `"hello"` memory contains:
* `'h'`
* `'e'`
* `'l'`
* `'l'`
* `'o'`
* `'\0'`

> Note: most of the string functions require `#include <cstring>`

## 2. Declare strings

```cpp
char a[] = "hello";
char b[20] = "world";
char c[] = { 'h', 'i', '\0' };
```

Important:

```cpp
char bad[] = { 'h', 'i' };   // not a valid C string
```

Without `'\0'`, functions for C strings will not work correctly.

## 3. Print string

```cpp
#include <iostream>

char text[] = "hello";
std::cout << text << '\n';
```

## 4. Get string length

Use `strlen` from `<cstring>`:

```cpp
#include <cstring>

char text[] = "hello";
size_t len = strlen(text);   // 5
```

`strlen` does not count the final `'\0'`.

## 5. Access characters

```cpp
char text[] = "hello";

char a = text[0];   // 'h'
char b = text[1];   // 'e'
```

Change character:

```cpp
text[0] = 'H';
```

## 6. Copy string

Use `strcpy`:

```cpp
#include <cstring>

char src[] = "hello";
char dst[20];

strcpy(dst, src);
```

After copy, `dst` contains `"hello"`.

Safe rule:
* destination array must be large enough

Wrong:

```cpp
char dst[3];
strcpy(dst, "hello");   // overflow
```

Limited copy with `strncpy`:

```cpp
char dst[6];
strncpy(dst, "hello", 5);
dst[5] = '\0';
```

Important:
* `strncpy` copies at most given number of characters
* `strncpy` does not always add final `'\0'`
* often you need to add `'\0'` manually

## 7. Concatenate strings

Use `strcat`:

```cpp
#include <cstring>

char text[20] = "hello";
strcat(text, " world");
```

Now `text` contains `"hello world"`.

Again, destination must have enough free space.

Limited concatenation with `strncat`:

```cpp
char text[20] = "hello";
strncat(text, " world!!!", 6);
```

Now `text` becomes `"hello world"`.

## 8. Compare strings

Use `strcmp`:

```cpp
#include <cstring>

int r1 = strcmp("abc", "abc");   // 0
int r2 = strcmp("abc", "abd");   // less than 0
int r3 = strcmp("abd", "abc");   // greater than 0
```

Do not compare C strings with `==` if you want to compare text content.

Wrong idea:

```cpp
char a[] = "cat";
char b[] = "cat";
if (a == b) {
    // will never get here
}
```

Need:

```cpp
if (strcmp(a, b) == 0) {
    // equal text
}
```

Limited compare with `strncmp`:

```cpp
int r = strncmp("abcdef", "abcxyz", 3);   // 0
```

This compares only the first `n` characters.

## 9. Search inside string

Find character with `strchr`:

```cpp
char text[] = "hello";
char* p = strchr(text, 'l');
```

`p` points to the first `'l'` inside the string.

Find substring with `strstr`:

```cpp
char text[] = "hello world";
char* p = strstr(text, "world");
```

`p` points to `"world"` inside `text`.

## 10. Input string

One old style is reading into a char array:

```cpp
char name[50];
std::cin >> name;
```

This stops at first space.

For line input:

```cpp
std::cin.getline(name, 50);
```

## 11. Common functions

From `<cstring>`:
* `strlen` - string length
* `strcpy` - copy string
* `strncpy` - copy not more than `n` characters
* `strcat` - concatenate strings
* `strncat` - append not more than `n` characters
* `strcmp` - compare strings
* `strncmp` - compare first `n` characters
* `strchr` - find character
* `strstr` - find substring

## 12. Important limitations

Old C strings:
* have fixed size
* can overflow if buffer is too small
* must end with `'\0'`
* are less convenient than `std::string`

They are still useful when working with:
* old C libraries
* low-level code
* fixed-size buffers
