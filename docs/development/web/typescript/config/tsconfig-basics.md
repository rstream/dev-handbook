# tsconfig basics

[← back](../index.md)

`tsconfig.json` marks a TypeScript project and stores compiler settings.

## Commands

```sh
npx tsc
npx tsc --noEmit
npx tsc --project tsconfig.app.json
```

`--noEmit` checks types without writing JS output.

## Basic config

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ES2020",
    "rootDir": "./src",
    "outDir": "./dist"
  },
  "include": ["src"]
}
```

Key fields:

- `compilerOptions` - TypeScript compiler settings.
- `target` - JavaScript language version emitted by the compiler.
- `module` - JavaScript module format for emitted files.
- `rootDir` - root folder used for building output paths.
- `outDir` - folder where compiled files are written.
- `include` - files to be compiled by TSC.

## Files included

If `files`, `include`, and `exclude` are omitted, TypeScript includes supported files in the config folder and subfolders.

```json
{
  "include": ["src/**/*.ts", "src/**/*.tsx"],
  "exclude": ["node_modules", "dist"]
}
```

`exclude` only filters files discovered by `include`. It does not block imports from included files.

## `files` vs `include`

```json
{
  "files": ["src/main.ts"]
}
```

Use `files` for a fixed small list. Use `include` for normal projects.
