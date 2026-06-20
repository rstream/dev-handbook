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
