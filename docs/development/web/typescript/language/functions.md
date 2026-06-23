# Functions

[← back](../index.md)

## Parameters and return

Regular function:

```ts
function add(a: number, b: number): number {
    return a + b;
}
```

Arrow function:

```ts
const multiply = (a: number, b: number): number => {
    return a * b;
};
```

## Optional and default params

```ts
function greet(name = "Guest") {
    return `Hello, ${name}`;
}

function findUser(id: number, includePosts?: boolean) {
    // ...
}
```

An optional `includePosts` param has type `boolean | undefined`

## Function type

```ts
type Handler = (event: MouseEvent) => void;

const onClick: Handler = event => {
    console.log(event.clientX);
};
```

## Overloads

```ts
// overload signatures
function get(id: number): User;
function get(name: string): User[];

// implementation
function get(value: number | string): User | User[] {
    throw new Error("todo");
}
```

Use overloads when return type depends on parameter shape.
