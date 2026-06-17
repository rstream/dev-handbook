# Directories

[← back](../index.md)

Use `node:fs/promises` to create, read, rename, and delete directories.

## Summary

- [Create directory](#create-directory) - make one folder
- [Create nested directories](#create-nested-directories) - use `recursive`
- [Read directory](#read-directory) - list entries
- [Read directory with types](#read-directory-with-types) - separate files and folders
- [Rename or move directory](#rename-or-move-directory) - change directory path
- [Delete empty directory](#delete-empty-directory) - remove one empty folder
- [Delete directory recursively](#delete-directory-recursively) - remove folder and content
- [Check that directory exists](#check-that-directory-exists) - use `access()`

## Create directory

```js
import { mkdir } from 'node:fs/promises';

await mkdir('uploads');
```

## Create nested directories

Use `recursive: true` when parent directories may not exist.

```js
import { mkdir } from 'node:fs/promises';

await mkdir('uploads/images/avatars', { recursive: true });
```

## Read directory

```js
import { readdir } from 'node:fs/promises';

const entries = await readdir('uploads');

console.log(entries);
// ['image.png', 'avatars']
```

## Read directory with types

Use `withFileTypes: true` to get `Dirent` objects.

```js
import { readdir } from 'node:fs/promises';

const entries = await readdir('uploads', { withFileTypes: true });

for (const entry of entries) {
  console.log(entry.name);
  console.log(entry.isFile());
  console.log(entry.isDirectory());
}
```

## Rename or move directory

```js
import { rename } from 'node:fs/promises';

await rename('uploads', 'public/uploads');
```

## Delete empty directory

```js
import { rmdir } from 'node:fs/promises';

await rmdir('empty-folder');
```

## Delete directory recursively

Use `rm()` with `recursive: true` for a directory with content.

```js
import { rm } from 'node:fs/promises';

await rm('old-folder', { recursive: true });
```

Use `force: true` when it is okay if the directory does not exist.

```js
await rm('old-folder', { recursive: true, force: true });
```

## Check that directory exists

```js
import { access } from 'node:fs/promises';

async function directoryExists(dirPath) {
  try {
    await access(dirPath);
    return true;
  } catch {
    return false;
  }
}

console.log(await directoryExists('uploads'));
```
