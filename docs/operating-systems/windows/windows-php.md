# PHP for Windows

[← back](index.md)

## Download and install PHP

### Download PHP

Download PHP for Windows:  
https://www.php.net/downloads.php?os=windows

* Choose "x64 Thread Safe" version for Win x64.
* Download zip (named like **php-8.5.5-Win32-vs17-x64.zip**)

### Install PHP

* Unpack zip to `C:\Soft\PHP` or similar place
* Add this folder to `PATH`
```sh
setx PATH "C:\Soft\PHP;%PATH%"
```