# Files in C style

[← back](index.md)

## 1. Idea

Old C-style file work usually uses:
* `FILE*` from `<cstdio>`
* metadata functions from `<sys/stat.h>`
* directory functions from OS-specific headers

This style is low-level and portable only partly. File metadata and directory operations often depend on OS.

## 2. Open file

```cpp
#include <cstdio>

FILE* f = fopen("data.txt", "r");
```

Where:
* `"data.txt"` - file path
* `"r"` - open mode

Return value:
* pointer to opened file on success
* `nullptr` on error

Common modes:
* `"r"` - read text file
* `"w"` - write text file, recreate file
* `"a"` - append to file
* `"rb"` - read binary file
* `"wb"` - write binary file

Always check result:

```cpp
if (f == nullptr) {
    // open failed
}
```

## 3. Read file

Read line:

```cpp
char buf[256];
fgets(buf, sizeof(buf), f);
```

Parameters of `fgets(buf, sizeof(buf), f)`:
* `buf` - destination char array
* `sizeof(buf)` - maximum number of characters to read
* `f` - opened file

Return value:
* pointer to `buf` on success
* `nullptr` on end of file or error

`fgets` reads one text line or stops earlier if buffer limit is reached.

Read binary block:

```cpp
char buf[128];
size_t n = fread(buf, 1, sizeof(buf), f);
```

Parameters of `fread(buf, 1, sizeof(buf), f)`:
* `buf` - destination memory
* `1` - size of one element in bytes
* `sizeof(buf)` - number of elements to read
* `f` - opened file

Return value:
* number of elements actually read

In this example `fread` returns number of bytes read, because one element has size `1`.

If result is less than requested:
* file may have ended
* or read error happened

## 4. Write file

Write text:

```cpp
fputs("hello\n", f);
fprintf(f, "value = %d\n", 123);
```

Write binary block:

```cpp
int x = 42;
fwrite(&x, sizeof(x), 1, f);
```

Parameters of `fwrite(&x, sizeof(x), 1, f)`:
* `&x` - source memory address
* `sizeof(x)` - size of one element
* `1` - number of elements to write
* `f` - opened file

Return value:
* number of elements actually written

## 5. Close file

```cpp
fclose(f);
```

Return value:
* `0` on success
* `EOF` on error

## 6. Create file

Usually file is created by opening it for writing:

```cpp
FILE* f = fopen("new.txt", "w");
if (f != nullptr) {
    fclose(f);
}
```

## 7. Delete file

Use `remove`:

```cpp
#include <cstdio>

int rc = remove("old.txt");
```

`rc == 0` means success.

Return value:
* `0` on success
* non-zero on error

## 8. Check file existence

One common old way is `stat`:

```cpp
#include <sys/stat.h>

struct stat st;
bool exists = (stat("data.txt", &st) == 0);
```

Parameters of `stat("data.txt", &st)`:
* `"data.txt"` - path to file or directory
* `&st` - address of structure that receives metadata

Return value:
* `0` on success
* non-zero on error

## 9. File size

With `stat`:

```cpp
struct stat st;
if (stat("data.txt", &st) == 0) {
    long long size = st.st_size;
}
```

Or with seek:

```cpp
fseek(f, 0, SEEK_END);
long size = ftell(f);
fseek(f, 0, SEEK_SET);
```

Where:
* `fseek(f, 0, SEEK_END)` - move file position to the end
* `ftell(f)` - get current byte position
* `fseek(f, 0, SEEK_SET)` - move back to file start

## 10. File metadata

With `stat` you can usually get:
* file size
* last modification time
* permissions / mode bits

Example:

```cpp
#include <sys/stat.h>
#include <ctime>

struct stat st;
if (stat("data.txt", &st) == 0) {
    long long size = st.st_size;
    std::time_t modified = st.st_mtime;
}
```

Important:
* creation time is not portable in old C API
* file attributes such as hidden / read-only are OS-specific
* on Windows these are often accessed through WinAPI

## 11. Directory exists

Directories can also be checked with `stat`:

```cpp
#include <sys/stat.h>

struct stat st;
bool exists = (stat("logs", &st) == 0);
bool isDir = exists && (st.st_mode & S_IFDIR);
```

## 12. Create directory

POSIX:

```cpp
#include <sys/stat.h>

mkdir("logs", 0755);
```

Parameters:
* `"logs"` - directory path
* `0755` - access mode on POSIX

Return value:
* `0` on success
* non-zero on error

Windows:

```cpp
#include <direct.h>

_mkdir("logs");
```

Return value:
* `0` on success
* `-1` on error

## 13. Delete directory

POSIX:

```cpp
#include <unistd.h>

rmdir("logs");
```

Return value:
* `0` on success
* non-zero on error

Windows:

```cpp
#include <direct.h>

_rmdir("logs");
```

Return value:
* `0` on success
* `-1` on error

Usually directory must be empty.

## 14. Summary

Old C-style approach is useful for:
* simple file reading and writing
* compatibility with old code
* low-level binary work

But for modern C++ code, streams and `std::filesystem` are usually more convenient.
