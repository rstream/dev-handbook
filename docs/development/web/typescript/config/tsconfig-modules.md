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
