# Unions and intersections

[← back](../index.md)

## Union

```ts
type Status = "idle" | "loading" | "success" | "error";

let status: Status = "idle";
```

`A | B` means one of several types.

## Intersection

```ts
type User = {
  id: number;
};

type WithName = {
  name: string;
};

type NamedUser = User & WithName;
```

`A & B` means all properties from both types.

## Discriminated union

```ts
type Result =
  | { ok: true; value: string }
  | { ok: false; error: string };

function show(result: Result) {
  if (result.ok) {
    return result.value;
  }

  return result.error;
}
```

Use a literal field to choose the correct branch.

This type means the same (first "|" is just a formatting trick):
```ts
type Result =
  { ok: true; value: string }
  | { ok: false; error: string };
```