# SQL aggregate functions

[← back](index.md)

Aggregate functions calculate one value from many rows.

They are usually used with `GROUP BY`:

```sql
SELECT
    customer_id,
    SUM(total) AS total_sum
FROM orders
GROUP BY customer_id;
```

`GROUP BY customer_id` creates one group for each customer.  
`SUM(total)` calculates the sum inside each group.

## 1. COUNT - count rows

Count all rows in a table:

```sql
SELECT COUNT(*) AS order_count
FROM orders;
```

`COUNT(*)` counts rows, even if some columns contain `NULL`.

Count orders for each customer:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count
FROM orders
GROUP BY customer_id;
```

Count only non-empty values:

```sql
SELECT COUNT(email) AS customers_with_email
FROM customers;
```

`COUNT(email)` ignores rows where `email` is `NULL`.

Count unique values:

```sql
SELECT COUNT(DISTINCT customer_id) AS unique_customers
FROM orders;
```

`DISTINCT` removes duplicates before counting.

## 2. SUM - sum of values

Calculate total quantity:

```sql
SELECT SUM(quantity) AS total_qty
FROM lines;
```

Calculate total quantity for each order:

```sql
SELECT
    order_id,
    SUM(quantity) AS total_qty
FROM lines
GROUP BY order_id;
```

`SUM` is useful for quantities, money, scores, stock, and other numeric values.

## 3. AVG - average value

Calculate average price:

```sql
SELECT AVG(price) AS avg_price
FROM products;
```

Calculate average line quantity for each order:

```sql
SELECT
    order_id,
    AVG(quantity) AS avg_qty
FROM lines
GROUP BY order_id;
```

`AVG` ignores `NULL` values.

## 4. MIN and MAX - smallest and largest value

Find the cheapest and most expensive product:

```sql
SELECT
    MIN(price) AS min_price,
    MAX(price) AS max_price
FROM products;
```

Find first and last order date for each customer:

```sql
SELECT
    customer_id,
    MIN(date) AS first_order_date,
    MAX(date) AS last_order_date
FROM orders
GROUP BY customer_id;
```

`MIN` and `MAX` work with numbers, dates, and text.

## 5. STRING_AGG / GROUP_CONCAT - join values into text

PostgreSQL:

```sql
SELECT
    order_id,
    STRING_AGG(product_name, ', ') AS products
FROM lines
GROUP BY order_id;
```

MySQL and SQLite:

```sql
SELECT
    order_id,
    GROUP_CONCAT(product_name, ', ') AS products
FROM lines
GROUP BY order_id;
```

These functions collect many text values into one string.

## 6. ARRAY_AGG - collect values into an array

PostgreSQL:

```sql
SELECT
    order_id,
    ARRAY_AGG(product_id) AS product_ids
FROM lines
GROUP BY order_id;
```

`ARRAY_AGG` is useful when the result should keep separate values, not one text string.

## 7. JSON_AGG - collect rows into JSON

PostgreSQL:

```sql
SELECT
    order_id,
    JSON_AGG(
        JSON_BUILD_OBJECT(
            'product_id', product_id,
            'quantity', quantity
        )
    ) AS lines
FROM lines
GROUP BY order_id;
```

`JSON_AGG` is useful when SQL prepares data for an API or application.

## 8. BOOL_AND and BOOL_OR - check conditions

PostgreSQL:

```sql
SELECT
    order_id,
    BOOL_AND(quantity > 0) AS all_quantities_positive,
    BOOL_OR(quantity >= 10) AS has_big_line
FROM lines
GROUP BY order_id;
```

`BOOL_AND` returns true only if all rows in the group match the condition.  
`BOOL_OR` returns true if at least one row in the group matches the condition.

## 9. GROUP BY - group by non-aggregate fields

If `SELECT` contains normal fields and aggregate functions, all normal fields must usually be in `GROUP BY`:

```sql
SELECT
    o.id AS tranid,
    c.name AS customer,
    o.date AS date,
    SUM(l.quantity) AS total_qty
FROM orders AS o
JOIN customers AS c ON c.id = o.customer_id
JOIN lines AS l ON l.order_id = o.id
GROUP BY o.id, c.name, o.date
ORDER BY c.name, o.date, total_qty;
```

Normal fields:

```sql
o.id, c.name, o.date
```

Aggregate field:

```sql
SUM(l.quantity)
```

The normal fields describe the group.  
The aggregate field calculates a value inside the group.

## 10. HAVING - filter groups

`WHERE` filters rows before grouping.  
`HAVING` filters groups after grouping.

Show only orders where total quantity is more than 10:

```sql
SELECT
    order_id,
    SUM(quantity) AS total_qty
FROM lines
GROUP BY order_id
HAVING SUM(quantity) > 10;
```

Use `WHERE` for normal columns:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count
FROM orders
WHERE date >= '2026-01-01'
GROUP BY customer_id;
```

Use `HAVING` for aggregate conditions:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 5;
```

## Common pattern

```sql
SELECT
    group_field,
    AGGREGATE_FUNCTION(value_field) AS result_name
FROM table_name
WHERE row_condition
GROUP BY group_field
HAVING aggregate_condition
ORDER BY result_name;
```

Execution idea:

1. `FROM` and `JOIN` choose tables.
2. `WHERE` filters source rows.
3. `GROUP BY` creates groups.
4. Aggregate functions calculate values for each group.
5. `HAVING` filters calculated groups.
6. `ORDER BY` sorts the final result.

## Quick reference

| Function | Meaning | Example |
| --- | --- | --- |
| `COUNT(*)` | Count rows | `COUNT(*) AS order_count` |
| `COUNT(column)` | Count non-null values | `COUNT(email) AS email_count` |
| `COUNT(DISTINCT column)` | Count unique values | `COUNT(DISTINCT customer_id)` |
| `SUM(column)` | Sum values | `SUM(quantity) AS total_qty` |
| `AVG(column)` | Average value | `AVG(price) AS avg_price` |
| `MIN(column)` | Smallest value | `MIN(date) AS first_date` |
| `MAX(column)` | Largest value | `MAX(date) AS last_date` |
| `STRING_AGG(column, ', ')` | Join text values in PostgreSQL | `STRING_AGG(name, ', ')` |
| `GROUP_CONCAT(column, ', ')` | Join text values in MySQL/SQLite | `GROUP_CONCAT(name, ', ')` |
| `ARRAY_AGG(column)` | Collect values into an array | `ARRAY_AGG(product_id)` |
| `JSON_AGG(value)` | Collect values into JSON | `JSON_AGG(line_data)` |
| `BOOL_AND(condition)` | True if all rows match | `BOOL_AND(is_paid)` |
| `BOOL_OR(condition)` | True if any row matches | `BOOL_OR(is_paid)` |
