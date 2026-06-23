# Utility types

[← back](../index.md)

Built-in helpers for transforming types.

## Object helpers

```ts
type User = {
    id: number;
    name: string;
    email: string;
};

type UserPatch = Partial<User>;
type UserPreview = Pick<User, "id" | "name">;
type UserWithoutEmail = Omit<User, "email">;
type ReadonlyUser = Readonly<User>;
```

`Partial<User>` makes all properties optional.

```ts
type UserPatch = {
    id?: number;
    name?: string;
    email?: string;
};
```

`Pick<User, "id" | "name">` creates a type with only selected properties.

```ts
type UserPreview = {
    id: number;
    name: string;
};
```

`Omit<User, "email">` creates a type without selected properties.

```ts
type UserWithoutEmail = {
    id: number;
    name: string;
};
```

`Readonly<User>` makes all properties readonly.

```ts
type ReadonlyUser = {
    readonly id: number;
    readonly name: string;
    readonly email: string;
};
```

## Records

```ts
type Role = "admin" | "user";

const labels: Record<Role, string> = {
    admin: "Admin",
    user: "User"
};
```

`Record<Role, string>` creates an object type where every `Role` key has a `string` value.

```ts
type Labels = {
    admin: string;
    user: string;
};
```

## Function helpers

```ts
function createUser(name: string) {
    return { id: 1, name };
}

type CreatedUser = ReturnType<typeof createUser>;
type CreateUserArgs = Parameters<typeof createUser>;
```

`ReturnType<typeof createUser>` gets the function return type.

```ts
type CreatedUser = {
    id: number;
    name: string;
};
```

`Parameters<typeof createUser>` gets function parameter types as a tuple.

```ts
type CreateUserArgs = [name: string];
```

## Nullable helpers

```ts
type Value = string | null | undefined;

type RequiredValue = NonNullable<Value>; // string
```

`NonNullable<Value>` removes `null` and `undefined`.
