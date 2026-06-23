# Streams

[← back](../index.md)

Streams process data in chunks.
Use them for large files so Node.js does not load the whole file into memory.

## Summary

- [Read stream](#read-stream) - read file chunks
- [Write stream](#write-stream) - write file chunks
- [Pipe streams](#pipe-streams) - connect read and write streams
- [Pipeline](#pipeline) - promise-based stream piping

## Read stream

```js
import fs from 'node:fs';

const stream = fs.createReadStream('large-file.txt', {
    encoding: 'utf8'
});

stream.on('data', (chunk) => {
    console.log(chunk);
});

stream.on('end', () => {
    console.log('Done');
});
```

### Set chunk size

```js
import fs from 'node:fs';

const stream = fs.createReadStream('large-file.txt', {
    encoding: 'utf8',
    highWaterMark: 8192 // default is 65536
});
```

`highWaterMark` is set in bytes, not chars.


## Write stream

```js
import fs from 'node:fs';

const stream = fs.createWriteStream('output.txt', {
    encoding: 'utf8'
});

stream.write('First line\n');
stream.write('Second line\n');
stream.end();
```

## Pipe streams

Use `pipe()` to send data from a readable stream to a writable stream.
> Note: `encoding` is not set - using `Buffer` chunks. This is a preferred format for copying files.

```js
import fs from 'node:fs';

const source = fs.createReadStream('large-file.txt');
const target = fs.createWriteStream('large-file-copy.txt');

source.pipe(target);
```

## Pipeline

Use `pipeline()` when you want promise-based error handling.

```js
import fs from 'node:fs';
import { pipeline } from 'node:stream/promises';

await pipeline(
    fs.createReadStream('large-file.txt'),
    fs.createWriteStream('large-file-copy.txt')
);
```
