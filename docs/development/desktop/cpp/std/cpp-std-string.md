# std::string in C++

[← back](../index.md)

Use `std::string` for normal text in modern C++.
It stores text, knows its own length, and can grow when you append more characters.

## Summary

- [Include header](#include-header) - use `#include <string>`
- [Declare string](#declare-string) - create empty strings and strings with text
- [Read and print](#read-and-print) - output strings and read user input
- [Length](#length) - get number of characters with `size()` or `length()`
- [Check empty string](#check-empty-string) - check if a string has no characters
- [Access characters](#access-characters) - read and change characters by index
- [Concatenate strings](#concatenate-strings) - join strings with `+` and `+=`
- [Compare strings](#compare-strings) - compare text content with `==`, `!=`, `<`
- [Find text](#find-text) - search with `find()`
- [Substring](#substring) - copy part of a string with `substr()`

## Include header

`std::string` is declared in `<string>`.

```cpp
#include <string>
```

For input and output you usually also need `<iostream>`.

```cpp
#include <iostream>
#include <string>
```

## Declare string

```cpp
std::string name;
std::string text = "hello";
std::string copy(text);
```

An empty string contains no characters.

```cpp
std::string empty = "";
```

## Read and print

Print a string:

```cpp
std::string text = "hello";
std::cout << text << '\n';
```

Read one word:

```cpp
std::string name;
std::cin >> name;
```

Read a whole line:

```cpp
std::string line;
std::getline(std::cin, line);
```

`std::cin >> name` stops at the first space.
`std::getline()` reads the whole line.

## Length

Use `size()` to get the number of characters.

```cpp
std::string text = "hello";
int len = text.size();   // 5
```

`length()` does the same thing.

```cpp
int len = text.length();
```

## Check empty string

Use `empty()` to check if a string has no characters.

```cpp
std::string text = "";

if (text.empty()) {
    std::cout << "string is empty\n";
}
```

## Access characters

Index starts from `0`.

```cpp
std::string text = "hello";

char first = text[0];   // 'h'
text[0] = 'H';
```

Be careful with indexes.
Accessing outside the string is an error.

## Concatenate strings

Use `+` to create a new string.

```cpp
std::string first = "hello";
std::string second = "world";

std::string result = first + " " + second;
```

Use `+=` to append to an existing string.

```cpp
std::string text = "hello";
text += " world";
```

## Compare strings

`std::string` compares text content with normal operators.

```cpp
std::string a = "cat";
std::string b = "cat";

if (a == b) {
    std::cout << "same\n";
}
```

Other useful comparisons:

```cpp
if (a != b) {
    std::cout << "different\n";
}

if (a < b) {
    std::cout << "a goes before b\n";
}
```

## Find text

Use `find()` to search for a character or substring.

```cpp
std::string text = "hello world";

size_t pos = text.find("world");
```

If the text was found, `find()` returns its position.
If it was not found, it returns `std::string::npos`.

```cpp
if (pos != std::string::npos) {
    std::cout << "found at " << pos << '\n';
}
```

## Substring

Use `substr()` to copy part of a string.

```cpp
std::string text = "hello world";
std::string part = text.substr(6, 5);   // "world"
```

Arguments:

- first number - start index
- second number - number of characters
