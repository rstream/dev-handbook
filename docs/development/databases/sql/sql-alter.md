# SQL: change Tables

[← back](index.md)

## 1. Rename Table

```sql
ALTER TABLE goods
RENAME TO offers;
```

## 2. Add columns

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

## 3. Delete columns

Delete a column:
```sql
ALTER TABLE products
DROP COLUMN web_url;
```

Safely delete a column (only in separate queries):
```sql
ALTER TABLE products
DROP COLUMN IF EXISTS web_url;
```

## 4. Rename columns

```sql
ALTER TABLE offers
RENAME COLUMN value TO price;
```
Rename 2 columns
```sql
ALTER TABLE offers
RENAME COLUMN price TO cost;

ALTER TABLE offers
RENAME COLUMN description TO "desc"; -- "desc" is a reserved word - so only in quotes
```