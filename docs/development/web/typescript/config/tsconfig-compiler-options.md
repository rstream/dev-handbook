# Compiler options

[← back](../index.md)

Common options worth recognizing.

## Language level

```json
{
    "compilerOptions": {
        "target": "ES2022",
        "lib": ["ES2022", "DOM"]
    }
}
```

`target` controls emitted JS syntax. `lib` controls available global types.
Neither setting installs polyfills or adds APIs to the runtime.

### Browser defaults

For browser code, `lib` can be omitted:

```json
{
    "compilerOptions": {
        "target": "ES2022"
    }
}
```

TypeScript selects default libraries based on `target`, including ECMAScript APIs and browser globals such as `window` and `document`.
It does not write a `lib` array into `tsconfig.json`.

For example, with `target: "ES2022"`, the default `lib.es2022.full.d.ts` references:

- `ES2022` - standard JavaScript APIs, including earlier ECMAScript libraries.
- `DOM` - browser APIs such as `window` and `document`.
- `DOM.Iterable` and `DOM.AsyncIterable` - iteration declarations for DOM APIs.
- `WebWorker.ImportScripts` - the worker `importScripts()` declaration.
- `ScriptHost` - Windows Script Host declarations.

The exact defaults depend on the TypeScript version and target.
An explicit `lib` replaces this default selection; for example, `["ES2022", "DOM"]` does not automatically add `DOM.Iterable`.

See the TypeScript reference for [`lib`](https://www.typescriptlang.org/tsconfig/lib.html).

### Node.js without DOM types

For server code, specify `lib` explicitly to exclude browser globals:

```json
{
    "compilerOptions": {
        "target": "ES2022",
        "lib": ["ES2022"],
        "types": ["node"]
    }
}
```

Install Node.js declarations:

```sh
npm install -D @types/node
```

`lib` supplies standard JavaScript types; `types: ["node"]` includes Node.js globals such as `process` and `Buffer`.
The [`types` option](https://www.typescriptlang.org/tsconfig/types.html) selects packages contributing global declarations independently of `lib`.

```ts
console.log(process.version); // OK: declared by @types/node
window.location.href; // Error: Cannot find name 'window'
document.title; // Error: Cannot find name 'document'
```

This catches accidental DOM usage unless other declarations explicitly introduce those globals or reference the DOM library.
APIs also supported by Node.js, such as `fetch()`, can still be available through `@types/node`.

## Type checking

```json
{
    "compilerOptions": {
        "strict": true,
        "noUncheckedIndexedAccess": true,
        "exactOptionalPropertyTypes": true
    }
}
```

Use `strict` as the baseline. Add extra checks when the project can tolerate more explicit code.

## JS interop

```json
{
    "compilerOptions": {
        "allowJs": true,
        "checkJs": false,
        "esModuleInterop": true,
        "allowSyntheticDefaultImports": true
    }
}
```

`allowJs` includes `.js` files. `checkJs` type-checks them.

## Speed and library checks

```json
{
    "compilerOptions": {
        "skipLibCheck": true,
        "incremental": true
    }
}
```

`skipLibCheck` skips checking `.d.ts` internals from dependencies, but their public types are still used.
