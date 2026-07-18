# Check and create PostgreSQL database

[← back](../index.md)

## Summary

- [Check database existence](#check-database-existence) - query `pg_database` to check whether `testdb` exists
- [Create database if missing](#create-database-if-missing) - create `testdb` only when it does not exist

## Check database existence

To check whether database `testdb` exists, connect to an existing database first.
Usually this is the default `postgres` database.

```php
$pdo = new PDO(
    'pgsql:host=localhost;port=5432;dbname=postgres',
    'postgres',
    '0000'
);

$stmt = $pdo->prepare("
    SELECT 1
    FROM pg_database
    WHERE datname = :dbname
");

$stmt->execute([
    'dbname' => 'testdb',
]);

$databaseExists = $stmt->fetchColumn() !== false;
```

If `fetchColumn()` returns `false`, the database was not found.

## Create database if missing

```php
if (!$databaseExists) {
    $pdo->exec('CREATE DATABASE testdb');
}
```

Full example:

```php
$pdo = new PDO(
    'pgsql:host=localhost;port=5432;dbname=postgres',
    'postgres',
    '0000'
);

$stmt = $pdo->prepare("
    SELECT 1
    FROM pg_database
    WHERE datname = :dbname
");

$stmt->execute([
    'dbname' => 'testdb',
]);

$databaseExists = $stmt->fetchColumn() !== false;

if (!$databaseExists) {
    $pdo->exec('CREATE DATABASE testdb');
}
```

`CREATE DATABASE` creates a new database, so the connection must be opened to another existing database, not to `testdb`.
