# Modules

[← back](../index.md)

Module settings decide how imports are understood and emitted.

## Bundler apps

```json
{
    "compilerOptions": {
        "module": "ESNext",
        "moduleResolution": "Bundler",
        "noEmit": true
    }
}
```

Use this for Vite, Webpack, Rollup, and similar tools when TypeScript only checks types.

## Node ESM

```json
{
    "compilerOptions": {
        "module": "NodeNext",
        "moduleResolution": "NodeNext"
    }
}
```

This follows Node rules and uses `package.json` `"type"` to decide ESM vs CommonJS.

## Rewrite relative import extensions

Use `rewriteRelativeImportExtensions` (TypeScript 5.7+) to write `.ts` extensions in source imports and get `.js` extensions in the JavaScript emitted by `tsc`.

```json
{
    "compilerOptions": {
        "module": "NodeNext",
        "moduleResolution": "NodeNext",
        "rewriteRelativeImportExtensions": true
    }
}
```

For an ESM project (`"type": "module"` in `package.json`):

```ts
// Source: main.ts
import { createUser } from "./users.ts";

createUser();
```

```js
// Output: main.js
import { createUser } from "./users.js";

createUser();
```

This rewrites relative paths starting with `./` or `../`. It also handles `.mts` → `.mjs`, `.cts` → `.cjs`, and `.tsx` → `.js` (or `.jsx` with `jsx: "preserve"`). It does not add extensions to extensionless imports or rewrite package names and `paths` aliases.

`allowImportingTsExtensions` alone permits TypeScript extensions in imports but does not rewrite them. With `rewriteRelativeImportExtensions: true`, you do not need to enable it separately. JavaScript output must be enabled to get the rewritten imports (`noEmit: true` only checks types).

See the [TypeScript option reference](https://www.typescriptlang.org/tsconfig/rewriteRelativeImportExtensions.html).

## CommonJS output

```json
{
    "compilerOptions": {
        "module": "CommonJS",
        "target": "ES2020"
    }
}
```

Useful for older Node tooling.

## Type-only imports

```ts
import type { User } from "./types";
import { createUser } from "./users";
```

`import type` is removed from JS output.
