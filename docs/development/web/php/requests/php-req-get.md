# `$_GET` in PHP

[← back](../index.md)

`$_GET` contains query parameters from the URL.

Example URL:

```text
/search.php?q=php&page=2
```

PHP can read these values like this:

```php
$query = $_GET['q'] ?? '';
$page = (int) ($_GET['page'] ?? 1);
```

## Common example

```php
<?php
$category = $_GET['category'] ?? 'all';
?>

<h1>Category: <?= htmlspecialchars($category) ?></h1>
```

If the user opens:

```text
/products.php?category=laptops
```

then `$category` will contain `laptops`.

## Notes

- `$_GET` is used for filters, search, pagination, and other small values in the URL
- values from `$_GET` are strings by default
- a missing key should be handled with `??`
- output should be escaped with `htmlspecialchars()`

## Check that a parameter exists

```php
if (isset($_GET['id'])) {
    $id = (int) $_GET['id'];
}
```
