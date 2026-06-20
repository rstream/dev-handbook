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

## Minimal config

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "strict": true,
    "noEmit": true
  },
  "include": ["src"]
}
```

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
