# Generics

[← back](../index.md)

Generics let a type depend on another type.

## Function generic

```ts
function first<T>(items: T[]): T | undefined {
  return items[0];
}

const name = first(["Ann", "Bob"]); // string | undefined
```

## Constraints

```ts
function getId<T extends { id: number }>(item: T) {
  return item.id;
}
```

`extends` limits what `T` can be.

## Default type

```ts
type ApiResponse<T = unknown> = {
  data: T;
};
```

## Generic object type

```ts
type Option<T> = {
  label: string;
  value: T;
};
```

## Generic components

```ts
type ListProps<T> = {
  items: T[];
  render: (item: T) => string;
};
```
