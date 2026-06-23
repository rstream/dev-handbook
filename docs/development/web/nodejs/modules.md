# Modules

[← back](index.md)

Modules split code into separate files and make values reusable.
Node.js supports two module systems: ESM and CommonJS.

## Summary

- [ESM vs CommonJS](#esm-vs-commonjs) - two module systems in Node.js
- [Enable ESM](#enable-esm) - use `"type": "module"`
- [Named export in ESM](#named-export-in-esm) - export several values by name
- [Default export in ESM](#default-export-in-esm) - export one main value
- [Mixed import in ESM](#mixed-import-in-esm) - import default and named values together
- [CommonJS exports](#commonjs-exports) - export values with `module.exports`
- [CommonJS require](#commonjs-require) - import values with `require()`
- [File extensions](#file-extensions) - local ESM imports need extensions

## ESM vs CommonJS

ESM is the modern JavaScript module system.
It uses `import` and `export`.

```js
// math.js
export function add(a, b) {
    return a + b;
}

// app.js
import { add } from './math.js';
```

CommonJS is the older Node.js module system.
It uses `require()` and `module.exports`.

```js
// math.cjs
module.exports = {
    add(a, b) {
        return a + b;
    }
};

// app.cjs
const { add } = require('./math.cjs');
```

Use ESM for new code.
Know CommonJS because older Node.js projects and many examples still use it.

## Enable ESM

Set `"type": "module"` in `package.json`.

```json
{
    "type": "module"
}
```

Then Node.js treats `.js` files as ES modules.

## Named export in ESM

Use named exports when a file exposes several values.

`math.js`:

```js
export function add(a, b) {
    return a + b;
}

export function subtract(a, b) {
    return a - b;
}
```

`app.js`:

```js
import { add, subtract } from './math.js';

console.log(add(2, 3));
// 5

console.log(subtract(5, 2));
// 3
```

You can rename named imports:

```js
import { add as sum } from './math.js';

console.log(sum(2, 3));
// 5
```

You can also export several existing values with one `export` statement.

`math.js`:

```js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

const PI = 3.14;

export {
    add,
    subtract,
    PI
};
```

`app.js`:

```js
import { add, subtract, PI } from './math.js';

console.log(add(2, 3));
// 5

console.log(subtract(5, 2));
// 3

console.log(PI);
// 3.14
```

## Default export in ESM

Use a default export when a file exposes one main value.

`logger.js`:

```js
export default function log(message) {
    console.log(`[app] ${message}`);
}
```

`app.js`:

```js
import log from './logger.js';

log('Started');
// [app] Started
```

The import name can be any name:

```js
import writeLog from './logger.js';

writeLog('Started');
// [app] Started
```

## Mixed import in ESM

A file can export one default value and several named values.

`user-service.js`:

```js
export const tableName = 'users';

export function findUser(id) {
    return { id, name: 'Alice' };
}

export default function createUser(name) {
    return { id: 1, name };
}
```

`app.js`:

```js
import createUser, { findUser, tableName } from './user-service.js';

console.log(tableName);
// users

console.log(findUser(1));
// { id: 1, name: 'Alice' }

console.log(createUser('Bob'));
// { id: 1, name: 'Bob' }
```

## CommonJS exports

Export several values:

`math.cjs`:

```js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

module.exports = {
    add,
    subtract
};
```

Export one main value:

`logger.cjs`:

```js
module.exports = function log(message) {
    console.log(`[app] ${message}`);
};
```

## CommonJS require

Import several exported values:

```js
const { add, subtract } = require('./math.cjs');

console.log(add(2, 3));
// 5

console.log(subtract(5, 2));
// 3
```

Import one main exported value:

```js
const log = require('./logger.cjs');

log('Started');
// [app] Started
```

## File extensions

In ESM, include file extensions for local imports.

```js
import { add } from './math.js';
```

Not:

```js
import { add } from './math';
```

In CommonJS, extensionless local imports often work:

```js
const { add } = require('./math.cjs');
const { add } = require('./math');
```

Prefer explicit extensions in docs and examples.
