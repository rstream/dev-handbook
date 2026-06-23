# Type narrowing

[← back](../index.md)

Narrowing turns a broad type into a more specific type inside a block.

## `typeof`

```ts
function format(value: string | number) {
    if (typeof value === "number") {
        return value.toFixed(2);
    }

    return value.toUpperCase();
}
```

## `in`

```ts
type User = { name: string };
type Admin = { name: string; permissions: string[] };

function show(person: User | Admin) {
    if ("permissions" in person) {
        return person.permissions.join(", ");
    }

    return person.name;
}
```

## Equality

```ts
type State = "open" | "closed";

function label(state: State) {
    if (state === "open") {
        return "Open";
    }

    return "Closed";
}
```

## Type predicate

```ts
function isString(value: unknown): value is string {
    return typeof value === "string";
}
```
