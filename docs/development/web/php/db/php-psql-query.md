# Simple query to PostgreSQL

[← back](../index.md)

## Summary

- [Run a query](#run-a-query) - `PDO`, `query()`, and `fetchAll()` connect and fetch rows
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

## Render query results

```php
<ul>
<?php foreach ($customers as $customer): ?>
    <li><?= htmlspecialchars($customer['name']) ?> (<?= htmlspecialchars($customer['location']) ?>)</li>
<?php endforeach; ?>
</ul>
```
