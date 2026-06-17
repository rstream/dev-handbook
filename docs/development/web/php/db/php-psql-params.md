# Query parameters in PDO

[← back](../index.md)

Use query parameters when a query contains user input or values from variables.
Do not concatenate values directly into SQL strings.

## Summary

- [Prepare a query](#prepare-a-query) - `prepare()` creates a statement with placeholders
- [Pass parameters to `execute()`](#pass-parameters-to-execute) - `execute([...])` is the common short form
- [Bind parameters manually](#bind-parameters-manually) - `bindParam()` binds variables before execution
- [Boolean parameters](#boolean-parameters) - boolean values should be bound with `PDO::PARAM_BOOL`
- [Which form to use](#which-form-to-use) - choose `execute([...])` by default, use `bindParam()` when binding is useful

## Prepare a query

Use named placeholders in the SQL query.

```php
$sql = '
SELECT id, name, email
FROM users
WHERE role = :role
  AND id > :min_id
';

$stmt = $pdo->prepare($sql);
```

Placeholders are not wrapped in quotes.
PDO sends values separately from the SQL text.

## Pass parameters to `execute()`

The simplest form is to pass an associative array to `execute()`.

```php
$stmt->execute([
    'role' => 'admin',
    'min_id' => 100,
]);

$users = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

This is usually enough for `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.

```php
$sql = '
INSERT INTO users (name, email)
VALUES (:name, :email)
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'name' => $name,
    'email' => $email,
]);
```

## Bind parameters manually

`bindParam()` binds a variable to a placeholder.
The variable is read when `execute()` runs.

```php
$sql = '
SELECT id, name
FROM users
WHERE id = :id
';

$stmt = $pdo->prepare($sql);

$id = 10;
$stmt->bindParam('id', $id, PDO::PARAM_INT);
$stmt->execute();

$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

`bindParam()` can be useful when the same prepared statement is executed several times with changed variable values.

```php
$sql = '
INSERT INTO tags (name)
VALUES (:name)
';

$stmt = $pdo->prepare($sql);
$stmt->bindParam('name', $name, PDO::PARAM_STR);

$name = 'php';
$stmt->execute();

$name = 'postgresql';
$stmt->execute();
```

## Boolean parameters

Do not pass boolean parameters through the `execute([...])` array.
In PDO this form does not let you specify the parameter type, and PostgreSQL boolean values can be passed incorrectly.

Bind boolean values explicitly with `PDO::PARAM_BOOL`.

```php
$sql = '
SELECT id, name
FROM users
WHERE active = :active
';

$stmt = $pdo->prepare($sql);

$active = true;
$stmt->bindParam('active', $active, PDO::PARAM_BOOL);
$stmt->execute();

$users = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

## Which form to use

Prefer `execute([...])` for ordinary string and integer parameters.
It is shorter and easier to read.

Use `bindParam()` when you need explicit parameter types, especially for boolean values, or when the same statement is executed repeatedly with changed variables.

Common parameter types:

| Type | Use for |
| --- | --- |
| `PDO::PARAM_STR` | strings |
| `PDO::PARAM_INT` | integers |
| `PDO::PARAM_BOOL` | booleans |
| `PDO::PARAM_NULL` | `null` |
