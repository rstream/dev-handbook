# SQL numeric functions

[← back](index.md)

Numeric functions calculate or change one numeric value.

They are often used in `SELECT`:

```sql
SELECT
    name,
    price,
    ROUND(price, 2) AS rounded_price
FROM products;
```

## 1. ROUND - round a number

Round price to 2 digits after the point:

```sql
SELECT
    name,
    ROUND(price, 2) AS rounded_price
FROM products;
```

Round average price:

```sql
SELECT ROUND(AVG(price), 2) AS avg_price
FROM products;
```

`ROUND(value, digits)` rounds a number to the specified number of digits.

## 2. FLOOR - round down

```sql
SELECT
    name,
    FLOOR(price) AS price_floor
FROM products;
```

`FLOOR` returns the largest integer that is not greater than the value.

## 3. CEIL / CEILING - round up

```sql
SELECT
    name,
    CEIL(price) AS price_ceil
FROM products;
```

`CEIL` returns the smallest integer that is not less than the value.

Some databases also support the full name:

```sql
SELECT CEILING(price) AS price_ceil
FROM products;
```

## 4. TRUNC - cut digits without rounding

PostgreSQL:

```sql
SELECT
    name,
    TRUNC(price, 2) AS truncated_price
FROM products;
```

`TRUNC(value, digits)` cuts the number to the specified number of digits without rounding.

## 5. ABS - absolute value

```sql
SELECT
    ABS(balance) AS positive_balance
FROM accounts;
```

`ABS` removes the minus sign from a number.

## Quick reference

| Function | Meaning | Example |
| --- | --- | --- |
| `ROUND(value, digits)` | Round to N digits | `ROUND(price, 2)` |
| `FLOOR(value)` | Round down | `FLOOR(price)` |
| `CEIL(value)` | Round up | `CEIL(price)` |
| `CEILING(value)` | Round up | `CEILING(price)` |
| `TRUNC(value, digits)` | Cut digits without rounding | `TRUNC(price, 2)` |
| `ABS(value)` | Absolute value | `ABS(balance)` |
