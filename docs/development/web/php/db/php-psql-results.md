# Query results in PDO

[← back](../index.md)

After `query()` or `execute()`, choose how to read the result.
The right method depends on what kind of SQL query was executed.

## Summary

- [Read many rows](#read-many-rows) - `fetchAll()` returns an array of rows
- [Read one row](#read-one-row) - `fetch()` returns one row or `false`
- [Read one value](#read-one-value) - `fetchColumn()` returns a single column value
- [Check changed rows](#check-changed-rows) - `rowCount()` is useful for `INSERT`, `UPDATE`, and `DELETE`
- [Which method to use](#which-method-to-use) - choose by expected result shape

## Read many rows

Use `fetchAll()` when the query can return multiple rows.

```php
$sql = '
SELECT id, name, email
FROM users
WHERE active = true
ORDER BY name
';

$stmt = $pdo->query($sql);
$users = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

`PDO::FETCH_ASSOC` returns each row as an associative array.

```php
foreach ($users as $user) {
    echo $user['name'];
}
```

## Read one row

Use `fetch()` when the query should return one row.

```php
$sql = '
SELECT id, name, email
FROM users
WHERE id = :id
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'id' => $id,
]);

$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

If no row is found, `fetch()` returns `false`.

```php
if ($user === false) {
    echo 'User not found';
}
```

## Read one value

Use `fetchColumn()` when the query returns one value, such as a count or an id.

```php
$sql = '
SELECT COUNT(*)
FROM users
WHERE active = true
';

$stmt = $pdo->query($sql);
$count = (int) $stmt->fetchColumn();
```

It is also useful with `RETURNING id`.

```php
$sql = '
INSERT INTO users (name, email)
VALUES (:name, :email)
RETURNING id
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'name' => $name,
    'email' => $email,
]);

$id = (int) $stmt->fetchColumn();
```

## Check changed rows

For `INSERT`, `UPDATE`, and `DELETE`, there may be no result rows to fetch.
Use `rowCount()` when you need to know whether the query changed any rows.

```php
$sql = '
UPDATE users
SET email = :email
WHERE id = :id
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'email' => $email,
    'id' => $id,
]);

$updated = $stmt->rowCount() > 0;
```

Use the boolean result in application logic.

```php
if ($updated) {
    echo 'User was updated';
} else {
    echo 'Nothing changed';
}
```

## Which method to use

| Query result | Method |
| --- | --- |
| Many rows | `fetchAll(PDO::FETCH_ASSOC)` |
| One row | `fetch(PDO::FETCH_ASSOC)` |
| One value | `fetchColumn()` |
| Changed rows for `INSERT`, `UPDATE`, `DELETE` | `rowCount()` |

Do not use `fetchAll()` automatically for every query.
Use the method that matches the expected result.
