# Config file scope

[← back](../index.md)

TypeScript project scope is based on the selected `tsconfig.json`.

## Config discovery

Running `tsc` without `--project` searches for `tsconfig.json` in the current directory, then parent directories.

```sh
npx tsc
npx tsc -p tsconfig.json
npx tsc -p packages/app
```

`-p packages/app` means "use `packages/app/tsconfig.json`".

## Relative paths

Paths inside a config are relative to the config file itself.

```json
{
  "include": ["src"],
  "compilerOptions": {
    "outDir": "dist"
  }
}
```

Here `src` and `dist` are resolved near this `tsconfig.json`.

## Imported files

If an included file imports another file, that imported file becomes part of the program too.

```ts
// src/main.ts
import { format } from "../scripts/format";
```

Even if `scripts` is not in `include`, `scripts/format.ts` can still be type-checked because it is imported.

## Multiple configs

Common pattern:

```text
tsconfig.json
tsconfig.app.json
tsconfig.node.json
```

Use separate configs when browser code, Node scripts, tests, or build output need different options.
