# Files

[← back](../index.md)

Use `node:fs/promises` for regular async file operations.

## Summary

- [Read text file](#read-text-file) - read file content as string
- [Read binary file](#read-binary-file) - read file content as `Buffer`
- [Write file](#write-file) - create or replace a file
- [Append file](#append-file) - add content to the end
- [Copy file](#copy-file) - duplicate a file
- [Rename or move file](#rename-or-move-file) - change file path
- [Delete file](#delete-file) - remove a file
- [Check that file exists](#check-that-file-exists) - use `access()`

## Read text file

```js
import { readFile } from 'node:fs/promises';

const text = await readFile('notes.txt', 'utf8');

console.log(text);
```

## Read binary file

```js
import { readFile } from 'node:fs/promises';

const data = await readFile('image.png');

console.log(data.length);
// size in bytes
```

## Write file

`writeFile()` creates a file or replaces its content.

```js
import { writeFile } from 'node:fs/promises';

await writeFile('notes.txt', 'Hello\n', 'utf8');
```

## Append file

```js
import { appendFile } from 'node:fs/promises';

await appendFile('notes.txt', 'Next line\n', 'utf8');
```

## Copy file

```js
import { copyFile } from 'node:fs/promises';

await copyFile('notes.txt', 'notes-copy.txt');
```

## Rename or move file

`rename()` changes a file path.
If the new path is in another folder, it moves the file.

```js
import { rename } from 'node:fs/promises';

await rename('notes-copy.txt', 'archive/notes-copy.txt');
```

## Delete file

```js
import { unlink } from 'node:fs/promises';

await unlink('old-notes.txt');
```

## Check that file exists

Use `access()` to check whether a path can be accessed.

```js
import { access } from 'node:fs/promises';

async function fileExists(filePath) {
  try {
    await access(filePath);
    return true;
  } catch {
    return false;
  }
}

console.log(await fileExists('notes.txt'));
```
