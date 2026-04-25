# Preparing data before rendering

[← back](index.md)

Templates should mostly render data, not build it.
Prepare values before including the HTML template.

## Prefer this

```php
<?php
$pageTitle = 'Users';
$visibleUsers = array_filter($users, fn ($user) => $user['active']);

require 'users.php';
```

```php
<h1><?= htmlspecialchars($pageTitle) ?></h1>
<ul>
    <?php foreach ($visibleUsers as $user): ?>
        <li><?= htmlspecialchars($user['name']) ?></li>
    <?php endforeach; ?>
</ul>
```

## Avoid this

```php
<ul>
    <?php foreach ($users as $user): ?>
        <?php if ($user['active'] && $user['age'] >= 18): ?>
            <li><?= htmlspecialchars($user['name']) ?></li>
        <?php endif; ?>
    <?php endforeach; ?>
</ul>
```

Complex filtering, sorting, and mapping are easier to test and maintain outside the template.
