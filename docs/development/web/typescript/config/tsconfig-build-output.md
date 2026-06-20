# Build output

[← back](../index.md)

These options matter when `tsc` emits files.

## Output folders

```json
{
  "compilerOptions": {
    "rootDir": "src",
    "outDir": "dist"
  }
}
```

`rootDir` is the source root. `outDir` is where JS files are written.

## Source maps

```json
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```

Source maps connect emitted JS back to `.ts` files in debugging tools.

## Declaration files

```json
{
  "compilerOptions": {
    "declaration": true,
    "declarationMap": true,
    "emitDeclarationOnly": false
  }
}
```

Use declarations for libraries. Apps usually do not need them.

## No output

```json
{
  "compilerOptions": {
    "noEmit": true
  }
}
```

Use when a bundler handles JS output.
