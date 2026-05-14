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

## 5. Change column definition

### Change column type

```sql
ALTER TABLE products
ALTER COLUMN price TYPE NUMERIC(12,2);
```

### Set or remove `NOT NULL`

Set `NOT NULL`:
```sql
ALTER TABLE products
ALTER COLUMN name SET NOT NULL;
```
> Note: this will fail if the column already contains `NULL` values

Remove `NOT NULL`:
```sql
ALTER TABLE products
ALTER COLUMN name DROP NOT NULL;
```

### Set or remove default value

Set default value:
```sql
ALTER TABLE products
ALTER COLUMN quantity SET DEFAULT 0;
```

Remove default value:
```sql
ALTER TABLE products
ALTER COLUMN quantity DROP DEFAULT;
```

### Add `UNIQUE`

Add a unique constraint for one column:
```sql
ALTER TABLE users
ADD CONSTRAINT users_login_unique UNIQUE (login);
```
> Note: this will fail if the column already contains duplicate values

`UNIQUE` does not make the column `NOT NULL`, so if the field must be mandatory, add both:
```sql
ALTER TABLE users
ALTER COLUMN login SET NOT NULL;

ALTER TABLE users
ADD CONSTRAINT users_login_unique UNIQUE (login);
```
