# PHP + PostgreSQL setup

[← back](../index.md)

## Summary

- [Make sure PostgreSQL service is running](#postgresql-service) - check the database service before PHP setup
- [Edit php.ini](#edit-php-ini) - enable PostgreSQL extensions for PHP

## <a id="postgresql-service"></a>Make sure PostgreSQL service is running

### Windows

Open Windows services:
```sh
services.msc
```
Make sure `postgresql-x64-18` service is running.

## <a id="edit-php-ini"></a>Edit php.ini

### Prepare the file

Check the PHP installation folder. e.g. `C:\Soft\PHP`.  
If there's no `php.ini` make it as a copy of `php.ini-development`.  

### Set extension directory

To set the extension directory uncomment this line:

#### Windows

```ini
extension_dir = "ext"
```

### Enable PostgreSQL extension

You need to enable the following features:
* PDO (PHP Data Objects) for PostgreSQL (interface for working with DB)
* PostgreSQL extension

Uncomment the following lines:

```ini
extension=pdo_pgsql
extension=pgsql
```
