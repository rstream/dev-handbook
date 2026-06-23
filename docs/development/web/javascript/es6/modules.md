# Modules

[← back](../index.md)

ES modules split JavaScript into files with explicit imports and exports.
They also change how the file is executed.

## Summary

- [Named export](#named-export) - export several values by name
- [Default export](#default-export) - export one main value
- [Import everything](#import-everything) - import a module namespace
- [Side-effect import](#side-effect-import) - run a module without importing values
- [Module behavior](#module-behavior) - strict mode, defer, top-level await, `this`
- [File extensions](#file-extensions) - browser imports need exact paths

## Named export

Use named exports when a module exposes several values.

```js
// math.js
export function add(a, b) {
    return a + b;
}

export const PI = 3.14;
```

```js
// app.js
import { add, PI } from './math.js';
```

You can rename imports.

```js
import { add as sum } from './math.js';
```

## Default export

Use default export when a module has one main value.

```js
// logger.js
export default function log(message) {
    console.log(message);
}
```

```js
// app.js
import log from './logger.js';
```

## Import everything

```js
import * as math from './math.js';

math.add(2, 3);
```

## Side-effect import

Use a side-effect import when the module only needs to run.

```js
import './setup.js';
```

## Module behavior

### Include module in HTML

In browser HTML, use `type="module"`.

```html
<script type="module" src="app.js"></script>
```

### Always strict

Modules always run in strict mode.

```js
this;
// undefined at the top level
```

### Always defer

Module scripts are deferred by default.
They run after HTML parsing, similar to classic scripts with `defer`.

### Top level variables are not on `window`

Top-level variables are module-scoped.
They are not added to `window`.

```js
const appName = 'Demo';

window.appName;
// undefined
```

### Top level await

Modules can use top-level `await`.

```js
const response = await fetch('/config.json');
const config = await response.json();
```

## File extensions

In browsers, local module imports need exact file paths.

```js
import './utils.js';
```

This is wrong in browser modules:

```js
import './utils';
```

More browser-specific notes: [`<script type="module">`](../type-module.md).
