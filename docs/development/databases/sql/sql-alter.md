# SQL: change Tables

[← back](index.md)

## 1. Add columns

Add 2 new columns to the Table
```sql
ALTER TABLE products
ADD COLUMN description TEXT,
ADD COLUMN free_shipping BOOLEAN;
```

Add a mandatory column:
```sql
ALTER TABLE products
ADD COLUMN web_url TEXT NOT NULL DEFAULT '';
```
> Note: when adding a mandatory (NOT NULL) column you should specify a default value

## 2. Delete columns

Delete a column:
```sql
ALTER TABLE products
DROP COLUMN web_url;
```

Safely delete a column:
```sql
ALTER TABLE products
DROP COLUMN IF EXISTS web_url;
```