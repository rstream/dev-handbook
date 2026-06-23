# Type annotations

[← back](../index.md)

Type annotations are written after values.

```ts
const name: string = "Ann";
let count: number = 0;
let active: boolean = true;
```

## Prefer inference when obvious

```ts
const name = "Ann"; // string
const count = 0; // number
```

Add annotations at boundaries: function params, public APIs, parsed data, shared objects.

## Function return types

```ts
function formatPrice(value: number): string {
    return `$${value.toFixed(2)}`;
}
```

Return types are often inferred, but explicit returns help public functions.

## Type assertion

```ts
const input = document.querySelector("input") as HTMLInputElement;
```

Assertion means "trust me". It does not validate at runtime.
