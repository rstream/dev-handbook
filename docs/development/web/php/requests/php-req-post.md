# `$_POST` in PHP

[← back](../index.md)

`$_POST` contains form data sent with the HTTP `POST` method.

## Summary

- [Basic form](#basic-form) - send fields with `method="post"`
- [Common example](#common-example) - read and print submitted data with `htmlspecialchars()`
- [Notes](#notes) - common rules for `$_POST`
- [Check that a field exists](#check-that-a-field-exists) - `isset()` checks optional fields and `trim()` cleans values
- [Check that the form was submitted](#check-that-the-form-was-submitted) - detect POST requests and clean values with `trim()`

## <a id="basic-form"></a>Basic form

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

## <a id="common-example"></a>Common example

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

## <a id="notes"></a>Notes

- `$_POST` is usually used for form submission
- values from `$_POST` are strings by default
- a missing key should be handled with `??`
- output should be escaped with `htmlspecialchars()`
- input should be validated before saving or processing

## <a id="check-that-a-field-exists"></a>Check that a field exists

```php
if (isset($_POST['email'])) {
    $email = trim($_POST['email']);
}
```

## <a id="check-that-the-form-was-submitted"></a>Check that the form was submitted

```php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $message = trim($_POST['message'] ?? '');
}
```
