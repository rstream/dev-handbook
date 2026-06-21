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

Using arrow function:
```ts
const first = <T>(items: T[]): T | undefined => {
  return items[0];
};
```

Type declaration:
```ts
type GenericFn = <T>(items: T[]) => T | undefined;
```

## Constraints

```ts
function getId<T extends { id: number }>(item: T) {
  return item.id;
}
```

`extends` limits what `T` can be (`T` must be an object with a mandatory key `type`)

## Default type

```ts
type ApiResponse<T = unknown> = {
  data: T;
};

const response: ApiResponse<string> = {
  data: "hello"
};
```

## Generic object type

```ts
type Option<T> = {
  label: string;
  value: T;
};
```

## Generic interface + class

```ts
interface Repository<T> {
  add(item: T): void;
  getAll(): T[];
}

class MemoryRepository<T> implements Repository<T> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  getAll(): T[] {
    return this.items;
  }
}

const users = new MemoryRepository<{ id: number; name: string }>();

users.add({ id: 1, name: "Ann" });
```

## Generic components

```ts
type ListProps<T> = {
  items: T[];
  render: (item: T) => string;
};
```
