# Extends and merging

[← back](../index.md)

`extends` allows one config to inherit another.

## Basic usage

```json
{
    "extends": "./tsconfig.base.json",
    "compilerOptions": {
        "noEmit": true
    },
    "include": ["src"]
}
```

## What is merged

`compilerOptions` are merged by property.

```json
{
    "compilerOptions": {
        "strict": true,
        "target": "ES2022"
    }
}
```

```json
{
    "extends": "./tsconfig.base.json",
    "compilerOptions": {
        "target": "ES2020"
    }
}
```

Result: `strict` stays enabled, `target` becomes `ES2020`.

## What is replaced

Top-level `files`, `include`, `exclude`, and `references` are replaced, not merged.

```json
{
    "extends": "./tsconfig.base.json",
    "include": ["src"]
}
```

If the base config had another `include`, it is ignored here.

## Relative paths in inherited configs

Relative paths are resolved relative to the config where they are written.

```json
{
    "compilerOptions": {
        "typeRoots": ["./types"]
    }
}
```

If this is `configs/base.json`, `./types` means `configs/types`.
