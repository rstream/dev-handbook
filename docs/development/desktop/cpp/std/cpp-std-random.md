# Random generation in C++

[← back](../index.md)

Use `<random>` when you need random numbers, random choices, test data, or simple generated identifiers.

Modern C++ random generation has two main parts:

* random engine - produces raw pseudo-random values
* distribution - converts engine output into values from a useful range

## Summary

- [Include header](#include-header) - use `#include <random>`
- [Random engine](#random-engine) - create and reuse `std::mt19937`
- [Random integer](#random-integer) - generate integers in a range
- [Random real number](#random-real-number) - generate floating-point values
- [Random character](#random-character) - choose one character from a string
- [Random string](#random-string) - generate a string character by character
- [Random password-like token](#random-password-like-token) - generate text from several character groups
- [Shuffle values](#shuffle-values) - randomize element order with `std::shuffle`
- [Important notes](#important-notes) - common mistakes and security notes

## Include header

Random utilities are declared in `<random>`.

```cpp
#include <random>
```

For examples below we also use `<iostream>` and `<string>`.

```cpp
#include <iostream>
#include <random>
#include <string>
```

## Random engine

Create a random engine once and reuse it.

```cpp
std::random_device rd;
std::mt19937 gen(rd());
```

`std::random_device` is used to get an initial seed.
`std::mt19937` is a common pseudo-random engine.

Do not create a new engine for every random value.
Create it once and pass it to distributions when you need values.

## Random integer

Use `std::uniform_int_distribution` for integers.

```cpp
std::random_device rd;
std::mt19937 gen(rd());

std::uniform_int_distribution<int> dist(1, 6);

int dice = dist(gen);

std::cout << dice << '\n';
```

Both limits are included.
`dist(1, 6)` can return `1`, `2`, `3`, `4`, `5`, or `6`.

## Random real number

Use `std::uniform_real_distribution` for floating-point numbers.

```cpp
std::random_device rd;
std::mt19937 gen(rd());

std::uniform_real_distribution<double> dist(0.0, 1.0);

double value = dist(gen);

std::cout << value << '\n';
```

This is useful for simulations, random percentages, simple game logic, and test data.

## Random character

To choose one character, generate a random index.

```cpp
std::random_device rd;
std::mt19937 gen(rd());

std::string letters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
std::uniform_int_distribution<int> dist(0, static_cast<int>(letters.size()) - 1);

char c = letters[dist(gen)];

std::cout << c << '\n';
```

The distribution chooses an index from the string.
Then the program takes the character at that index.

## Random string

A common real-life task is generating a random identifier, file suffix, invite code, or temporary username.

This example creates a random string from Latin letters, one character at a time.

```cpp
#include <iostream>
#include <random>
#include <string>

std::string randomString(int length, std::mt19937& gen)
{
    const std::string letters =
        "abcdefghijklmnopqrstuvwxyz"
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    std::uniform_int_distribution<int> dist(0, static_cast<int>(letters.size()) - 1);

    std::string result;

    for (int i = 0; i < length; i++) {
        result += letters[dist(gen)];
    }

    return result;
}

int main()
{
    std::random_device rd;
    std::mt19937 gen(rd());

    std::string name = randomString(12, gen);

    std::cout << name << '\n';

    return 0;
}
```

Example output:

```text
qHTmzVaKpLrx
```

Each run will usually print a different string.

## Random password-like token

For a more realistic generated text value, use several groups of characters.

```cpp
#include <iostream>
#include <random>
#include <string>

std::string randomToken(int length, std::mt19937& gen)
{
    const std::string chars =
        "abcdefghijklmnopqrstuvwxyz"
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        "0123456789";

    std::uniform_int_distribution<int> dist(0, static_cast<int>(chars.size()) - 1);

    std::string token;

    for (int i = 0; i < length; i++) {
        token += chars[dist(gen)];
    }

    return token;
}

int main()
{
    std::random_device rd;
    std::mt19937 gen(rd());

    std::cout << randomToken(16, gen) << '\n';

    return 0;
}
```

This is good for demos, test data, temporary names, and non-critical identifiers.

Do not use this example for real passwords, session IDs, password reset links, or API keys.
Security-sensitive tokens need cryptographically secure random generation.

## Shuffle values

`std::shuffle` randomizes order of elements in a container.

```cpp
#include <algorithm>
#include <iostream>
#include <random>
#include <vector>

int main()
{
    std::random_device rd;
    std::mt19937 gen(rd());

    std::vector<int> values = { 1, 2, 3, 4, 5 };

    std::shuffle(values.begin(), values.end(), gen);

    for (int value : values) {
        std::cout << value << ' ';
    }

    std::cout << '\n';

    return 0;
}
```

This is useful for cards, quiz questions, randomized tests, playlists, and game objects.

## Important notes

Prefer `<random>` over old `rand()`.
`rand()` has weak quality and awkward range handling.

Create the engine once and reuse it.
Creating and seeding an engine inside a tight loop can produce poor results and slower code.

Use the correct distribution:

* `std::uniform_int_distribution<int>` for integers
* `std::uniform_real_distribution<double>` for real numbers

Use random generation carefully in tests.
For repeatable tests, use a fixed seed.

```cpp
std::mt19937 gen(12345);
```

With a fixed seed, the program generates the same sequence every run.
