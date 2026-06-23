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

Used for object shapes, classes, and APIs that may be extended.

### General interface declaration

```ts
interface User {
    id: number;
    name: string;
    greet(): string;
}
```

### Interface for key-value object with any (string) keys

```ts
interface Scores {
    [name: string]: number;
}

const scores: Scores = {
    alice: 10,
    bob: 8,
};
```

### Interface for function

```ts
interface FormatName {
    (firstName: string, lastName: string): string;
}

const formatName: FormatName = (firstName, lastName) => {
    return `${firstName} ${lastName}`;
};
```

### Extending interfaces

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

### Declaration merging

Interfaces with the same name merge.

```ts
interface Window {
    appVersion: string;
}
```

Type aliases do not merge.
