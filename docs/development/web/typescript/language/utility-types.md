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

## Records

```ts
type Role = "admin" | "user";

const labels: Record<Role, string> = {
  admin: "Admin",
  user: "User"
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

## Nullable helpers

```ts
type Value = string | null | undefined;

type RequiredValue = NonNullable<Value>; // string
```
