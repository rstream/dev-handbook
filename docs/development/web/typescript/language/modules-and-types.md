# Modules and types

[← back](../index.md)

Types can be imported and exported like values.

## Exporting types

```ts
export type User = {
  id: number;
  name: string;
};

export interface Config {
  apiUrl: string;
}
```

## Type-only imports

```ts
import type { User } from "./user";
import { createUser } from "./user";
```

Use `import type` when the import is needed only by TypeScript.

## Re-exporting types

```ts
export type { User } from "./user";
export { createUser } from "./user";
```

## `typeof` for value types

```ts
const settings = {
  theme: "dark",
  pageSize: 20
};

type Settings = typeof settings;
```

`typeof` in a type position gets the type of a value.
