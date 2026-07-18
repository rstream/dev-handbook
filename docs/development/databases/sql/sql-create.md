# SQL: create table

[← back](index.md)

## Simple table with various types of fields

```sql
CREATE TABLE products (
	id SERIAL PRIMARY KEY,
	name TEXT NOT NULL,
	description TEXT,
	price NUMERIC(10,2) NOT NULL,
	quantity INT NOT NULL,
	added_on TIMESTAMP DEFAULT NOW()
);
```

## Create table only if it does not exist

Use `IF NOT EXISTS` when the script can be run more than once.

```sql
CREATE TABLE IF NOT EXISTS products (
	id SERIAL PRIMARY KEY,
	name TEXT NOT NULL,
	description TEXT,
	price NUMERIC(10,2) NOT NULL,
	quantity INT NOT NULL,
	added_on TIMESTAMP DEFAULT NOW()
);
```

If the table already exists, PostgreSQL skips creation instead of returning an error.

## Table with joins

```sql
CREATE TABLE roles (
	id SERIAL PRIMARY KEY,
	name VARCHAR(64) NOT NULL
);
```

```sql
CREATE TABLE users (
	id SERIAL PRIMARY KEY,
	name TEXT NOT NULL,
	email VARCHAR(64) UNIQUE,
	role_id INT REFERENCES roles(id),
	reg_date TIMESTAMP DEFAULT NOW()
);
```

## Check if a table exists

Use `information_schema.tables`:

```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
	AND table_name = 'products';
```

If the query returns a row, the table exists.

In PostgreSQL, you can also use `to_regclass()`:

```sql
SELECT to_regclass('public.products');
```

If the result is `public.products`, the table exists.
If the result is `null`, the table does not exist.
