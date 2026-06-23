# Path module

[← back](../index.md)

`node:path` works with filesystem paths as strings.
Use it instead of manual string concatenation.

## Summary

- [Import](#import) - load `node:path`
- [Join path parts](#join-path-parts) - build paths safely
- [Resolve absolute paths](#resolve-absolute-paths) - turn parts into an absolute path
- [Parse path parts](#parse-path-parts) - get directory, file name, extension
- [Normalize paths](#normalize-paths) - clean `.` and `..`
- [Platform-specific paths](#platform-specific-paths) - Windows and POSIX helpers

## Import

```js
import path from 'node:path';
```

## Join path parts

`path.join()` joins path parts and uses the correct separator for the operating system.

```js
const filePath = path.join('public', 'images', 'logo.png');

console.log(filePath);
// Windows: public\images\logo.png
// Linux/macOS: public/images/logo.png
```

Use it for relative paths:

```js
const configPath = path.join('config', 'app.json');
```

## Resolve absolute paths

`path.resolve()` returns an absolute path.
Relative parts are resolved from the current working directory.

```js
const fullPath = path.resolve('public', 'index.html');

console.log(fullPath);
```

With an absolute base:

```js
const fullPath = path.resolve('/app', 'public', 'index.html');
```

## Parse path parts

```js
const filePath = '/app/public/index.html';

console.log(path.dirname(filePath));
// /app/public

console.log(path.basename(filePath));
// index.html

console.log(path.extname(filePath));
// .html
```

`path.parse()` returns all main parts:

```js
const info = path.parse('/app/public/index.html');

console.log(info);
// {
//   root: '/',
//   dir: '/app/public',
//   base: 'index.html',
//   ext: '.html',
//   name: 'index'
// }
```

Build a path from parsed parts:

```js
const filePath = path.format({
    dir: '/app/public',
    name: 'index',
    ext: '.html'
});
```

## Normalize paths

`path.normalize()` cleans duplicate separators, `.` and `..`.

```js
const cleanPath = path.normalize('/app/public/../config/app.json');

console.log(cleanPath);
// /app/config/app.json
```

## Platform-specific paths

`path` uses the current operating system rules.

Use `path.win32` when you need Windows path rules on any OS:

```js
const dir = path.win32.dirname('C:\\app\\public\\index.html');
```

Use `path.posix` when you need POSIX path rules on any OS:

```js
const dir = path.posix.dirname('/app/public/index.html');
```
