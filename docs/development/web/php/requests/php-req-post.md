# `$_POST` in PHP

[← back](../index.md)

`$_POST` contains form data sent with the HTTP `POST` method.

## Basic form

```html
<form method="post" action="/post.php">
    <input type="text" name="username">
    <button type="submit">Send</button>
</form>
```

PHP can read the submitted value like this:

```php
$username = $_POST['username'] ?? '';
```

## Common example

```php
<form method="post" action="/post.php">
    <input type="email" name="email">
    <button type="submit">Save</button>
</form>
```

```php
<?php
$email = $_POST['email'] ?? '';
?>
<p><?= htmlspecialchars($email) ?></p>
```

## Notes

- `$_POST` is usually used for form submission
- values from `$_POST` are strings by default
- a missing key should be handled with `??`
- output should be escaped with `htmlspecialchars()`
- input should be validated before saving or processing

## Check that the form was submitted

```php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $message = trim($_POST['message'] ?? '');
}
```
