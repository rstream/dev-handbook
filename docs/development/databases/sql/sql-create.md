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
