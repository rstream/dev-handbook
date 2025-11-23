# C++ compilers for Windows

[← back](index.md)

There are 2 popular compilers you can use for C++ development.

## Install MinGW (GCC) compiler

Go to: [**www.winlibs.com**](https://www.winlibs.com)  
Scroll down to the **"MSVCRT runtime"** section.  
Look for the latest version — e.g.:

> **GCC 14.2.0** (with POSIX threads) + LLVM/Clang/LLD/LLDB 19.1.1 + MinGW-w64 12.0.0 (MSVCRT) — *release 2*

🔸 *Beginners:* choose the version **without LLVM/Clang/LLD/LLDB**.  
🔸 Unpack to a folder like: `C:\Soft\mingw64\`  
🔸 Add the `bin` subfolder to your **PATH**: `C:\Soft\mingw64\bin`

## Install Clang

Clang is a part of LLVM package. To install it visit LLVM download page:  
[https://releases.llvm.org/download.html](https://releases.llvm.org/download.html)

link to the latest version will look like:  
[https://github.com/llvm/llvm-project/releases/tag/llvmorg-18.1.8](https://github.com/llvm/llvm-project/releases/tag/llvmorg-18.1.8)

Find and download `LLVM-18.1.8-win64.exe`

> Note: During installation agree with adding LLVM to PATH (to make clang available at any place)