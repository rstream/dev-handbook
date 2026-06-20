# Interfaces and type aliases

[← back](../index.md)

Both describe shapes.

## Type alias

```ts
type User = {
  id: number;
  name: string;
};
```

Can name unions, primitives, tuples, and object shapes.

```ts
type ID = string | number;
type Point = [number, number];
```

## Interface

```ts
interface User {
  id: number;
  name: string;
}
```

Good for object shapes, classes, and APIs that may be extended.

## Extending

```ts
interface Admin extends User {
  permissions: string[];
}
```

With type aliases:

```ts
type Admin = User & {
  permissions: string[];
};
```

## Declaration merging

Interfaces with the same name merge.

```ts
interface Window {
  appVersion: string;
}
```

Type aliases do not merge.
