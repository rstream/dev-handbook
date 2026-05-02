# SQL queries (select)

[← back](index.md)

## 1. Select all columns

```sql
SELECT *
FROM products;
```

`*` means "all columns".

## 2. Select specific columns

```sql
SELECT id, name, price
FROM products;
```

Use this form when you do not need every column.

## 3. Rename columns with AS

```sql
SELECT id, name AS product_name, price AS cost
FROM products;
```

`AS` gives a temporary name in the result.

You can also rename the table:

```sql
SELECT p.id, p.name, p.price
FROM products AS p;
```

## 4. Filter rows with WHERE

Select only one product by ID:

```sql
SELECT id, name, price
FROM products
WHERE id = 1;
```

Select products cheaper than 500:

```sql
SELECT name, price
FROM products
WHERE price < 500;
```

Select products in a price range:

```sql
SELECT name, price
FROM products
WHERE price >= 100 AND price <= 1000;
```

Select products by name:

```sql
SELECT id, name
FROM products
WHERE name = 'laptop';
```

Select products with one of several names:

```sql
SELECT id, name, price
FROM products
WHERE name = 'laptop' OR name = 'desktop';
```

## 5. Join tables

Get users with their role names:

```sql
SELECT users.id, users.name, roles.name AS role_name
FROM users
JOIN roles ON users.role_id = roles.id;
```

The same query with short aliases:

```sql
SELECT u.id, u.name, r.name AS role_name
FROM users AS u
JOIN roles AS r ON u.role_id = r.id;
```

`JOIN` connects rows from two tables by related columns.

### Left join

Show all users, even if some users have no role:

```sql
SELECT u.id, u.name, r.name AS role_name
FROM users AS u
LEFT JOIN roles AS r ON u.role_id = r.id;
```

## 6. Arithmetic in SELECT

Add 20 to every price:

```sql
SELECT name, price, price + 20 AS new_price
FROM products;
```

Calculate price with 10 percent discount:

```sql
SELECT name, price, price * 0.9 AS discount_price
FROM products;
```

Calculate total value of stock:

```sql
SELECT name, price, quantity, price * quantity AS total_value
FROM products;
```

You can use `+`, `-`, `*`, `/` inside `SELECT`.
