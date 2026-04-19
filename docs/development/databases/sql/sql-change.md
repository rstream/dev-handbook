# SQL: change data in tables

[← back](index.md)

## 1. Insert new lines

Add 5 new products to the table
```sql
INSERT INTO products (name, price) VALUES
('laptop', 1000),
('desktop', 750),
('monitor', 300),
('keyboard', 110),
('mouse', 90);
```

## 2. Update existing lines

Set price `99` for ALL lines
```sql
UPDATE products
SET price = 99;
```

Change price to `100` for the 1st line (ID=1):
```sql
UPDATE products
SET price = 100
WHERE id = 1;
```

Change laptop price to `1050`
```sql
UPDATE products
SET price = 1050
WHERE name = 'laptop';
```

Change laptop name and price
```sql
UPDATE products
SET name = 'laptop (i7)', price = 1200
WHERE name = 'laptop';
```
Notes:
* no "TABLE" before table name
* no comma after the last column

## 3. Delete lines

Delete all lines (one by one - slow on big tables)
```sql
DELETE FROM products;
```
Delete all lines (at once - fast) and reset ID counter to 1
```sql
TRUNCATE TABLE products;
```

Delete all products with price below 100:
```sql
DELETE FROM products
WHERE price < 100;
```

