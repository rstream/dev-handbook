# File system basics

[← back](../index.md)

Node.js works with files and folders through built-in `node:fs` APIs.
For normal async operations, use `node:fs/promises`.

## Summary

- [API variants](#api-variants) - promise, callback, and sync APIs
- [Recommended style](#recommended-style) - use `fs/promises` by default
- [Text and Buffer](#text-and-buffer) - string data and binary data
- [Encoding](#encoding) - read text as `utf8`
- [Common errors](#common-errors) - handle missing files and permissions

## API variants

Promise API:

```js
import { readFile } from 'node:fs/promises';

const text = await readFile('data.txt', 'utf8');
```

Sync API:

```js
import { readFileSync } from 'node:fs';

const text = readFileSync('data.txt', 'utf8');
```

Callback API exists too, but it is mostly used in older code.

## Recommended style

Use `node:fs/promises` for regular file operations.

```js
import { readFile, writeFile } from 'node:fs/promises';

const text = await readFile('input.txt', 'utf8');

await writeFile('output.txt', text.toUpperCase());
```

Use `node:fs` for streams:

```js
import fs from 'node:fs';

const stream = fs.createReadStream('large-file.txt');
```

Avoid sync methods in servers because they block the event loop.

## Text and Buffer

Without encoding, `readFile()` returns a `Buffer`.

```js
import { readFile } from 'node:fs/promises';

const data = await readFile('image.png');

console.log(data);
// <Buffer ...>
```

With encoding, `readFile()` returns a string.

```js
const text = await readFile('notes.txt', 'utf8');

console.log(text);
// file text
```

## Encoding

Use `utf8` for normal text files.

```js
import { readFile, writeFile } from 'node:fs/promises';

const text = await readFile('input.txt', 'utf8');

await writeFile('output.txt', text, 'utf8');
```

## Common errors

File system operations can fail.

```js
import { readFile } from 'node:fs/promises';

try {
  const text = await readFile('missing.txt', 'utf8');
  console.log(text);
} catch (error) {
  if (error.code === 'ENOENT') {
    console.log('File does not exist');
  } else {
    throw error;
  }
}
```

Common error codes:

- `ENOENT` - file or directory does not exist
- `EACCES` - no permission
- `EISDIR` - expected file, got directory
- `ENOTDIR` - expected directory, got file
