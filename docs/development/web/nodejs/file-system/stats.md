# Stats

[← back](../index.md)

Use `stat()` to inspect a filesystem path.

## Summary

- [Get stats](#get-stats) - inspect one path
- [Check path type](#check-path-type) - file or directory
- [File size](#file-size) - size in bytes
- [Dates](#dates) - created, modified, and accessed times
- [Handle missing path](#handle-missing-path) - catch `ENOENT`

## Get stats

```js
import { stat } from 'node:fs/promises';

const info = await stat('notes.txt');

console.log(info);
```

## Check path type

```js
import { stat } from 'node:fs/promises';

const info = await stat('notes.txt');

console.log(info.isFile());
// true

console.log(info.isDirectory());
// false
```

## File size

`size` is in bytes.

```js
const info = await stat('image.png');

console.log(info.size);
// 24812
```

## Dates

```js
const info = await stat('notes.txt');

console.log(info.birthtime);
// creation time

console.log(info.mtime);
// last content modification time

console.log(info.atime);
// last access time
```

## Handle missing path

```js
import { stat } from 'node:fs/promises';

try {
    const info = await stat('missing.txt');
    console.log(info.isFile());
} catch (error) {
    if (error.code === 'ENOENT') {
        console.log('Path does not exist');
    } else {
        throw error;
    }
}
```
