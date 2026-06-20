# Strictness

[← back](../index.md)

`strict` enables the main safety checks.

```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

## Common strict errors

```ts
function greet(name: string | null) {
  return name.toUpperCase();
  // error: name can be null
}
```

Fix by narrowing:

```ts
function greet(name: string | null) {
  return name ? name.toUpperCase() : "Guest";
}
```

## Useful extra checks

```json
{
  "compilerOptions": {
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "noImplicitOverride": true
  }
}
```

`noUncheckedIndexedAccess` makes array/object indexing return possible `undefined`.

```ts
const names = ["Ann"];
const first = names[0]; // string | undefined
```

## Escape hatches

Prefer `unknown` over `any`.

```ts
const value: unknown = JSON.parse(text);
```

Use `any` only when type checking is intentionally disabled for that value.
