# Conditional blocks

[← back](index.md)

Use `if`, `elseif`, and `else` to render different HTML blocks.
The alternative template syntax is usually easier to read in mixed HTML/PHP files.

## if

```php
<?php if ($isLoggedIn): ?>
    <p>Welcome back.</p>
<?php endif; ?>
```

## if / else

```php
<?php if ($isLoggedIn): ?>
    <a href="/logout">Log out</a>
<?php else: ?>
    <a href="/login">Log in</a>
<?php endif; ?>
```

## if / elseif / else

```php
<?php if ($status === 'success'): ?>
    <p>Saved.</p>
<?php elseif ($status === 'warning'): ?>
    <p>Saved with warnings.</p>
<?php else: ?>
    <p>Save failed.</p>
<?php endif; ?>
```
