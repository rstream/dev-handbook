# Primitive and special types

[← back](../index.md)

## Primitives

```ts
let name: string = "Ann";
let age: number = 30;
let ready: boolean = true;
let id: symbol = Symbol("id");
let big: bigint = 100n;
```

## `null` and `undefined`

```ts
let value: string | null = null;
let missing: string | undefined = undefined;
```

With `strictNullChecks`, `null` and `undefined` must be listed explicitly.

## `any`

```ts
let value: any = JSON.parse(text);
value.missing.deep.call();
```

`any` disables type checking for that value.

## `unknown`

```ts
let value: unknown = JSON.parse(text);

if (typeof value === "string") {
    value.toUpperCase();
}
```

Use for values that need checking before use.  
`unknown` is safer than `any` and usually is recommended.

## `never` and `void`

```ts
function log(message: string): void {
    console.log(message);
}

function fail(message: string): never {
    throw new Error(message);
}
```

`void` means no useful return value.  
`never` means the function does not finish normally.
