# Simple query to PostgreSQL

[← back](../index.md)

## Summary

- [Run a query](#run-a-query) - `PDO`, `query()`, and `fetchAll()` connect and fetch rows
- [Use `exec()` for queries without result rows](#use-exec-for-queries-without-result-rows) - run `CREATE`, `INSERT`, `UPDATE`, or `DELETE`
- [Use `query()` for queries with result rows](#use-query-for-queries-with-result-rows) - run `SELECT` and read data from `$stmt`
- [Choose a statement method](#choose-a-statement-method) - `fetch()`, `fetchAll()`, `fetchColumn()`, and `rowCount()`
- [Render query results](#render-query-results) - `htmlspecialchars()` prints rows safely in HTML

## Run a query

Set up PDO connection (instance)
```php
// create a PDO instance
$pdo = new PDO(
    'pgsql:host=localhost;port=5432;dbname=crm1',
    'postgres',
    '0000'
);
```
Where:
* `localhost` - database host
* `5432` - host port
* `crm1` - database name
* `postgres` - user name
* `0000` - password

```php
$query =
'SELECT c.name AS name, l.name AS location
FROM customers AS c
JOIN locations AS l ON l.id = c.location_id';

// run query
$stmt = $pdo->query($query);

// transform results into an array of objects
$customers = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

## Use `exec()` for queries without result rows

Use `$pdo->exec()` when the query does not return rows.
It returns the number of changed rows, or `0` for some commands like `CREATE TABLE`.

```php
$sql = '
CREATE TABLE IF NOT EXISTS products (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    price NUMERIC(10,2) NOT NULL
)
';

$pdo->exec($sql);
```

`exec()` is useful for schema commands:

```php
$pdo->exec('DROP TABLE IF EXISTS old_products');
```

It is also useful for simple changes without user input:

```php
$changedRows = $pdo->exec("
    UPDATE products
    SET price = price * 1.10
");

echo $changedRows;
```

Do not put user input directly into SQL strings.
When the query uses user input, use `prepare()` and `execute()` instead.

## Use `query()` for queries with result rows

Use `$pdo->query()` when the query returns rows, usually with `SELECT`.
It returns a statement object in `$stmt`.

```php
$stmt = $pdo->query('SELECT id, name, price FROM products');

$products = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

Read one row:

```php
$stmt = $pdo->query('SELECT id, name, price FROM products LIMIT 1');

$product = $stmt->fetch(PDO::FETCH_ASSOC);
```

Read one value:

```php
$stmt = $pdo->query('SELECT COUNT(*) FROM products');

$count = (int) $stmt->fetchColumn();
```

## Choose a statement method

After `$pdo->query()` or `$stmt->execute()`, choose the method by the result you expect.

| Method | Use for | Result |
| --- | --- | --- |
| `$stmt->fetch(PDO::FETCH_ASSOC)` | one row | array or `false` |
| `$stmt->fetchAll(PDO::FETCH_ASSOC)` | many rows | array of rows |
| `$stmt->fetchColumn()` | one value from the first column | column value or `false` |
| `$stmt->rowCount()` | changed rows for `INSERT`, `UPDATE`, `DELETE` | number |

Examples:

```php
// one row
$stmt = $pdo->query('SELECT id, name FROM products LIMIT 1');
$product = $stmt->fetch(PDO::FETCH_ASSOC);
```

```php
// many rows
$stmt = $pdo->query('SELECT id, name FROM products');
$products = $stmt->fetchAll(PDO::FETCH_ASSOC);
```

```php
// one value
$stmt = $pdo->query('SELECT COUNT(*) FROM products');
$count = (int) $stmt->fetchColumn();
```

`fetchColumn()` reads column index `0` by default.
Pass a column index to read another column from the next row.
Column indexes start from `0`.

```php
$stmt = $pdo->query('SELECT id, name FROM products LIMIT 1');

$id = $stmt->fetchColumn(0);
```

```php
$stmt = $pdo->query('SELECT id, name FROM products LIMIT 1');

$name = $stmt->fetchColumn(1);
```

```php
// changed rows with prepared statement
$stmt = $pdo->prepare('UPDATE products SET price = :price WHERE id = :id');
$stmt->execute([
    'price' => 150,
    'id' => 1,
]);

$changedRows = $stmt->rowCount();
```

## Render query results

```php
<ul>
<?php foreach ($customers as $customer): ?>
    <li><?= htmlspecialchars($customer['name']) ?> (<?= htmlspecialchars($customer['location']) ?>)</li>
<?php endforeach; ?>
</ul>
```
