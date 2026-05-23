# Current location

[← back](../index.md)

There are two common "current" places in Node.js:

- current working directory - where the process was started from
- current module location - where the current `.js` file is located

## Summary

- [Current working directory](#current-working-directory) - `process.cwd()`
- [Current file URL](#current-file-url) - `import.meta.url`
- [Current file and folder](#current-file-and-folder) - convert `import.meta.url` to a path
- [Build paths from current folder](#build-paths-from-current-folder) - combine current folder and `path.join()`
- [URL and path conversion](#url-and-path-conversion) - convert between file URLs and paths

## Current working directory

`process.cwd()` returns the directory where the Node.js process was started.

```js
console.log(process.cwd());
```

Example:

```bash
cd D:\projects\my-app
node src/server.js
```

In this case:

```js
process.cwd();
// D:\projects\my-app
```

It does not mean "folder of the current file".
It means "folder from which the command was executed".

## Current file URL

In ES modules, use `import.meta.url` to get the current file URL.

```js
const currentFileUrl = import.meta.url;

console.log(currentFileUrl);
// file:///D:/projects/my-app/src/server.js
```

`import.meta.url` is a file URL, not a normal filesystem path.

## Current file and folder

Convert it with `fileURLToPath()`.

```js
import path from 'node:path';
import { fileURLToPath } from 'node:url';

const currentFile = fileURLToPath(import.meta.url);
const currentDir = path.dirname(currentFile);

// import.meta.url:
// file:///D:/projects/my-app/src/server.js

console.log(currentFile);
// D:\projects\my-app\src\server.js

console.log(currentDir);
// D:\projects\my-app\src
```

## Build paths from current folder

Use the current module folder as a stable base when reading files next to the current file.

```js
import path from 'node:path';
import { fileURLToPath } from 'node:url';

const currentFile = fileURLToPath(import.meta.url);
const currentDir = path.dirname(currentFile);

const configPath = path.join(currentDir, 'config.json');
```

Use `process.cwd()` when paths should be relative to the project command location:

```js
const configPath = path.join(process.cwd(), 'config.json');
```

Use `import.meta.url` when paths should be relative to the current file.

## URL and path conversion

Use `pathToFileURL()` to convert a filesystem path to a file URL.

```js
import { pathToFileURL } from 'node:url';

const fileUrl = pathToFileURL('D:\\projects\\my-app\\public\\index.html');

console.log(fileUrl.href);
// file:///D:/projects/my-app/public/index.html
```

Use `fileURLToPath()` to convert a file URL to a filesystem path.

```js
import { fileURLToPath } from 'node:url';

const filePath = fileURLToPath('file:///D:/projects/my-app/public/index.html');

console.log(filePath);
// D:\projects\my-app\public\index.html
```
