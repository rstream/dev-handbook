# SQL column types

[← back](index.md)

The sizes below apply to **PostgreSQL**. Other databases may use different sizes or type names.
Storage sizes describe individual values; table rows and indexes have additional overhead.

## 1. Numeric types

### Integer types

| Type | Storage | Range |
| --- | --- | --- |
| `SMALLINT` | 2 bytes (16 bits) | -32,768 to 32,767 |
| `INT`, `INTEGER` | 4 bytes (32 bits) | -2,147,483,648 to 2,147,483,647 |
| `BIGINT` | 8 bytes (64 bits) | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

`BIGINT` uses twice the value storage of `INT`, but supports a much larger range.
Use it when values may exceed the `INT` range.

### Floating point types

| Type | Storage | Decimal precision |
| --- | --- | --- |
| `REAL` | 4 bytes | About 6 significant digits |
| `DOUBLE PRECISION` | 8 bytes | About 15 significant digits |

`FLOAT(p)` selects precision in **binary digits**: `p` from 1 to 24 selects `REAL`,
and 25 to 53 selects `DOUBLE PRECISION`. `FLOAT` without `p` means `DOUBLE PRECISION`.
These types store approximate values, so use `NUMERIC` when exact decimal values are required.

### For money

`NUMERIC(p,s)` - decimal type for money  
p - total digits  
s - digits after the point

Storage is variable: 2 bytes per group of 4 decimal digits, plus 3–8 bytes of overhead.
The declared precision does not reserve a fixed amount of storage.
For example, `NUMERIC(12,2)` allows 10 digits before the decimal point and 2 after it.

## 2. String types

`CHAR(n)` - fixed length string  
`VARCHAR(n)` - variable length string with max length  
`TEXT` - long text without fixed limit

These types have **variable storage size**. `n` counts characters, not bytes;
for example, a UTF-8 character can take 1–4 bytes.
`CHAR(n)` pads shorter values with spaces; `VARCHAR(n)` stores only the actual string.
Short strings (up to 126 bytes) use the string's byte length plus 1 byte of overhead;
longer strings use 4 bytes of overhead before compression or out-of-line storage.
`TEXT` and `VARCHAR` without `n` have no declared length limit, but a value is limited to about 1 GB.

## 3. Date and time types

| Type | Storage | Description |
| --- | --- | --- |
| `DATE` | 4 bytes | Date only |
| `TIME` | 8 bytes | Time only, without time zone |
| `TIMESTAMP` | 8 bytes | Date + time, without time zone |
| `TIMESTAMPTZ` | 8 bytes | An instant stored in UTC and displayed in the session time zone |

`TIMESTAMPTZ` does not store the original time zone name or offset.
The optional precision in `TIME(p)`, `TIMESTAMP(p)` and `TIMESTAMPTZ(p)` is 0–6 fractional
second digits; reducing it does not reduce storage size.

## 4. Logical type

`BOOLEAN` - true / false, **1 byte**

## 5. Binary type

`BYTEA` - binary data (files, images, raw bytes)

Variable storage size: the actual data length plus 1 or 4 bytes of overhead,
before compression or out-of-line storage.

## 6. Auto-increment types

| Declaration | Underlying type | Value storage | Default generated range |
| --- | --- | --- | --- |
| `SMALLSERIAL` | `SMALLINT` | 2 bytes | 1 to 32,767 |
| `SERIAL` | `INT` | 4 bytes | 1 to 2,147,483,647 |
| `BIGSERIAL` | `BIGINT` | 8 bytes | 1 to 9,223,372,036,854,775,807 |

These declarations create integer columns with sequence-based defaults, rather than separate
storage types. The sequence is a separate database object with its own storage overhead.

## Example

```sql
CREATE TABLE users (
	id BIGSERIAL PRIMARY KEY,
	username VARCHAR(64) NOT NULL,
	bio TEXT,
	is_active BOOLEAN DEFAULT TRUE,
	balance NUMERIC(12,2) DEFAULT 0,
	avatar BYTEA,
	created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## References

PostgreSQL documentation:

* [Numeric and serial types](https://www.postgresql.org/docs/current/datatype-numeric.html)
* [Character types](https://www.postgresql.org/docs/current/datatype-character.html)
* [Date/time types](https://www.postgresql.org/docs/current/datatype-datetime.html)
* [Boolean type](https://www.postgresql.org/docs/current/datatype-boolean.html)
* [Binary types](https://www.postgresql.org/docs/current/datatype-binary.html)
