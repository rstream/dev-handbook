# Paths

[← back](../index.md)

Use path helpers when you need to split, inspect, or build filesystem path strings.
This page is only about paths, not reading files, writing files, or creating directories.

## Summary

- [Current file path](#current-file-path) - `__FILE__` and `__DIR__`
- [Directory name](#directory-name) - `dirname()` gets the parent path
- [Base name](#base-name) - `basename()` gets the last path part
- [Path information](#path-information) - `pathinfo()` splits a path into parts
- [Extension](#extension) - get only the file extension
- [Build paths](#build-paths) - join path parts with `DIRECTORY_SEPARATOR`
- [Current working directory](#current-working-directory) - `getcwd()` returns the process directory
- [Normalize an existing path](#normalize-an-existing-path) - `realpath()` resolves an existing path
- [Path separators](#path-separators) - `DIRECTORY_SEPARATOR` and `PATH_SEPARATOR`

## <a id="current-file-path"></a>Current file path

`__FILE__` is the full path to the current PHP file.
`__DIR__` is the directory that contains the current PHP file.

```php
echo __FILE__;
echo __DIR__;
```

Use `__DIR__` when you need a path relative to the script file.
This is usually more stable than relying on the current working directory.

```php
$configPath = __DIR__ . '/config/app.php';
```

## <a id="directory-name"></a>Directory name

`dirname()` returns the parent directory part of a path.

```php
$path = '/var/www/app/public/index.php';

echo dirname($path);     // /var/www/app/public
echo dirname($path, 2);  // /var/www/app
```

The second argument tells PHP how many parent levels to go up.

## <a id="base-name"></a>Base name

`basename()` returns the last part of a path.

```php
$path = '/var/www/app/public/index.php';

echo basename($path);         // index.php
echo basename($path, '.php'); // index
```

The optional suffix is removed only when the last path part ends with that suffix.

## <a id="path-information"></a>Path information

`pathinfo()` splits a path into common parts.

```php
$info = pathinfo('/var/www/app/public/index.php');

echo $info['dirname'];   // /var/www/app/public
echo $info['basename'];  // index.php
echo $info['extension']; // php
echo $info['filename'];  // index
```

You can also request one part directly.

```php
$name = pathinfo($path, PATHINFO_FILENAME);
$ext = pathinfo($path, PATHINFO_EXTENSION);
```

## <a id="extension"></a>Extension

Use `pathinfo($path, PATHINFO_EXTENSION)` when you only need the extension.

```php
$path = '/uploads/avatar.png';
$extension = pathinfo($path, PATHINFO_EXTENSION);

echo $extension; // png
```

The extension is returned without the dot.
If the path has no extension, PHP returns an empty string.

## <a id="build-paths"></a>Build paths

PHP has no common built-in `join_path()` function.
For simple local paths, concatenate parts with `DIRECTORY_SEPARATOR`.

```php
$path = __DIR__ . DIRECTORY_SEPARATOR . 'templates' . DIRECTORY_SEPARATOR . 'home.php';
```

When the project only runs on Unix-like paths, `/` is also commonly used.
PHP on Windows accepts `/` in most filesystem paths too.

```php
$path = __DIR__ . '/templates/home.php';
```

Avoid adding user input directly to a path without validation.

## <a id="current-working-directory"></a>Current working directory

`getcwd()` returns the current working directory of the running PHP process.

```php
$cwd = getcwd();

echo $cwd;
```

This is not always the same as `__DIR__`.
For web apps, `__DIR__` is usually better when you need paths relative to source files.

## <a id="normalize-an-existing-path"></a>Normalize an existing path

`realpath()` resolves `.` and `..`, symbolic links, and returns an absolute normalized path.

```php
$path = realpath(__DIR__ . '/../config/app.php');

if ($path !== false) {
    echo $path;
}
```

`realpath()` returns `false` when the path does not exist.
Do not use it for paths that you are about to create.

## <a id="path-separators"></a>Path separators

`DIRECTORY_SEPARATOR` is the separator inside one filesystem path.

```php
echo DIRECTORY_SEPARATOR; // "/" on Linux/macOS, "\\" on Windows
```

`PATH_SEPARATOR` separates multiple paths in one environment setting, such as `include_path`.

```php
echo PATH_SEPARATOR; // ":" on Linux/macOS, ";" on Windows
```
