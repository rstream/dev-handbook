# Files with streams in C++

[← back](../index.md)

## Summary

- [Idea](#idea)
- [Open file for reading](#open-file-for-reading)
- [Read file](#read-file)
- [Open file for writing](#open-file-for-writing)
- [Close file](#close-file)
- [Create file](#create-file)
- [Delete file](#delete-file)
- [Check existence](#check-existence)
- [File size](#file-size)
- [File metadata](#file-metadata)
- [Check if path is file or directory](#check-if-path-is-file-or-directory)
- [Create directory](#create-directory)
- [Delete directory](#delete-directory)
- [Example](#example)

## <a id="idea"></a>1. Idea

Modern C++ usually uses:
* file streams from `<fstream>`
* filesystem utilities from `<filesystem>`

This is more readable and more convenient than old `FILE*` API.

## <a id="open-file-for-reading"></a>2. Open file for reading

```cpp
#include <fstream>

std::ifstream in("data.txt");
if (!in) {
    // open failed
}
```

Where:
* `"data.txt"` - file path

State after open:
* stream is valid on success
* stream converts to `false` on error

## <a id="read-file"></a>3. Read file

Read one line:

```cpp
#include <string>

std::string line;
std::getline(in, line);
```

Parameters of `std::getline(in, line)`:
* `in` - input stream
* `line` - destination string

Return value:
* reference to stream

It can be used in conditions:

```cpp
while (std::getline(in, line)) {
    // read line by line
}
```

Read all lines:

```cpp
std::string line;
while (std::getline(in, line)) {
    // process line
}
```

Read binary data:

```cpp
std::ifstream in("data.bin", std::ios::binary);
char buf[128];
in.read(buf, sizeof(buf));
```

Parameters of `in.read(buf, sizeof(buf))`:
* `buf` - destination memory
* `sizeof(buf)` - number of bytes to read

Return value:
* reference to stream

Useful checks:

```cpp
std::streamsize n = in.gcount();
bool ok = static_cast<bool>(in);
```

Where:
* `gcount()` - number of bytes actually read by the last unformatted read
* stream may become false if requested amount could not be fully read

## <a id="open-file-for-writing"></a>4. Open file for writing

```cpp
#include <fstream>

std::ofstream out("data.txt");
out << "hello\n";
out << 123 << '\n';
```

Where:
* `"data.txt"` - file path
* `out << ...` - write text representation into file

Open in append mode:

```cpp
std::ofstream out("data.txt", std::ios::app);
```

Binary write:

```cpp
std::ofstream out("data.bin", std::ios::binary);
int x = 42;
out.write(reinterpret_cast<const char*>(&x), sizeof(x));
```

Parameters of `out.write(reinterpret_cast<const char*>(&x), sizeof(x))`:
* pointer to source bytes
* number of bytes to write

Return value:
* reference to stream

## <a id="close-file"></a>5. Close file

File streams can be closed explicitly with `close()`:

```cpp
in.close();
out.close();
```

What `close()` does:
* closes the file handle
* flushes pending output data for output streams
* disconnects the stream from the file

After `close()`, stream is no longer attached to the file.

Important:
* explicit `close()` is optional in many cases
* when stream object is destroyed, file is usually closed automatically
* explicit `close()` is useful when file must be closed before the end of scope

## <a id="create-file"></a>6. Create file

File is usually created automatically when opened by `std::ofstream`:

```cpp
std::ofstream out("new.txt");
```

If file does not exist, it is created.
If file exists, default `std::ofstream` mode usually truncates it.

## <a id="delete-file"></a>7. Delete file

Use `std::filesystem::remove`:

```cpp
#include <filesystem>

bool ok = std::filesystem::remove("old.txt");
```

Return value:
* `true` if something was removed
* `false` if path did not exist

## <a id="check-existence"></a>8. Check existence

```cpp
#include <filesystem>

namespace fs = std::filesystem;

bool exists = fs::exists("data.txt");
```

Return value:
* `true` if path exists
* `false` otherwise

## <a id="file-size"></a>9. File size

```cpp
std::uintmax_t size = fs::file_size("data.txt");
```

Return value:
* file size in bytes

Usually call it only after `fs::exists(...)` and for regular files.

## <a id="file-metadata"></a>10. File metadata

Modern standard library gives easy access to some metadata:

```cpp
auto status = fs::status("data.txt");
auto perms = status.permissions();
auto t = fs::last_write_time("data.txt");
```

Where:
* `status(...)` - gets file status information
* `permissions()` - returns access permission flags
* `last_write_time(...)` - returns last modification time

Available in portable C++:
* existence
* file size
* file type
* permissions
* last write time

Important:
* creation time is not provided portably by standard `std::filesystem`
* Windows file attributes such as hidden / archive are not standard C++ metadata
* for such attributes you usually need OS-specific API

## <a id="check-if-path-is-file-or-directory"></a>11. Check if path is file or directory

```cpp
bool isFile = fs::is_regular_file("data.txt");
bool isDir = fs::is_directory("logs");
```

Return value:
* `true` if path has requested type
* `false` otherwise

## <a id="create-directory"></a>12. Create directory

Create one directory:

```cpp
bool ok = fs::create_directory("logs");
```

Return value:
* `true` if directory was created
* `false` if it already existed

Create nested directories:

```cpp
bool ok = fs::create_directories("data/output/logs");
```

Return value:
* `true` if at least one directory was created
* `false` if full path already existed

## <a id="delete-directory"></a>13. Delete directory

Delete empty directory:

```cpp
bool ok = fs::remove("logs");
```

Return value:
* `true` if path was removed
* `false` if path did not exist

Delete directory with contents:

```cpp
std::uintmax_t n = fs::remove_all("logs");
```

Return value:
* number of removed files and directories

Be careful: `remove_all` deletes everything inside.

## <a id="example"></a>14. Example

```cpp
#include <filesystem>
#include <fstream>
#include <string>

namespace fs = std::filesystem;

int main() {
    if (!fs::exists("logs")) {
        fs::create_directory("logs");
    }

    std::ofstream out("logs/app.txt");
    out << "started\n";
    out.close();

    if (fs::exists("logs/app.txt")) {
        auto size = fs::file_size("logs/app.txt");
    }
}
```

## <a id="summary-2"></a>15. Summary

For modern C++ code:
* use `std::ifstream` for reading
* use `std::ofstream` for writing
* use `std::filesystem` for existence checks, sizes, times, and directories

This is usually the best default approach.
