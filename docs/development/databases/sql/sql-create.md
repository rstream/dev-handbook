# SQL: create table

[← back](index.md)

## Create table

### Simple table with various types of fields

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