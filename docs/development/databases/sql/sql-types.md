# SQL column types

[← back](index.md)

## 1. Numeric types

### Integer types

`SMALLINT` - small integer  
`INT`, `INTEGER` - normal integer  
`BIGINT` - big integer

### Floating point types

`REAL` - default floating point  
`FLOAT` - big floating point  
`DOUBLE PRECISION` - high precision floating point

### For money

`NUMERIC(p,s)` - decimal type for money  
p - total digits  
s - digits after the point

## 2. String types

`CHAR(n)` - fixed length string  
`VARCHAR(n)` - variable length string with max length  
`TEXT` - long text without fixed limit

## 3. Date and time types

`DATE` - date only  
`TIME` - time only  
`TIMESTAMP` - date + time  
`TIMESTAMPTZ` - date + time with timezone

## 4. Logical type

`BOOLEAN` - true / false

## 5. Binary type

`BYTEA` - binary data (files, images, raw bytes)

## 6. Auto-increment types

`SERIAL` - auto-increment integer (`INT`)  
`BIGSERIAL` - auto-increment big integer (`BIGINT`)

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
