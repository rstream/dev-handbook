# SQL: create database

[← back](index.md)

## Create a database

Create a new database:

```sql
CREATE DATABASE shop;
```

Database names are usually written in lowercase and without spaces.

## Create a database from terminal

Run the command from a terminal:

```bash
createdb shop
```

Or run SQL through `psql`:

```bash
psql -U postgres -c "CREATE DATABASE shop;"
```

## Connect to a database

Inside `psql`:

```sql
\c shop
```

From terminal:

```bash
psql -U postgres -d shop
```

## Check if a database exists

List all databases inside `psql`:

```sql
\l
```

Or filter by name:

```sql
\l shop
```

You can also check with SQL:

```sql
SELECT datname
FROM pg_database
WHERE datname = 'shop';
```

If the query returns a row, the database exists.

## Create only if the database does not exist

PostgreSQL does not support `CREATE DATABASE IF NOT EXISTS`.

Use a check first:

```sql
SELECT datname
FROM pg_database
WHERE datname = 'shop';
```

Then create the database only when the query returns no rows:

```sql
CREATE DATABASE shop;
```
