# Objects, arrays, tuples

[← back](../index.md)

## Object shapes

```ts
type User = {
    id: number;
    name: string;
    email?: string;
};
```

`?` means the property may be missing.

## Readonly

```ts
type User = {
    readonly id: number;
    name: string;
};
```

`readonly` prevents assignment through this type.

## Arrays

```ts
const names: string[] = ["Ann", "Bob"];
const scores: Array<number> = [10, 20];
```

Both forms are equivalent.

## Tuples

```ts
type Point = [number, number];

const point: Point = [10, 20];
```

Use tuples when position has meaning.

## Index signatures

```ts
type Scores = {
    [name: string]: number;
};
```

Use when keys are dynamic but values have one type. Variables of this type can have any number of keys (or have no keys).
