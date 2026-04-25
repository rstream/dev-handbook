# Looping over blocks

[← back](index.md)

Use loops when one HTML fragment must be rendered multiple times.
In templates, `foreach` is the most common choice.

## Render a list with `foreach`

```php
<ul>
    <?php foreach ($users as $user): ?>
        <li><?= htmlspecialchars($user['name']) ?></li>
    <?php endforeach; ?>
</ul>
```

## Use keys and values

```php
<ul>
    <?php foreach ($prices as $name => $price): ?>
        <li><?= htmlspecialchars($name) ?>: <?= htmlspecialchars((string) $price) ?></li>
    <?php endforeach; ?>
</ul>
```

## Show a fallback when the array is empty

```php
<?php if ($users): ?>
    <ul>
        <?php foreach ($users as $user): ?>
            <li><?= htmlspecialchars($user['name']) ?></li>
        <?php endforeach; ?>
    </ul>
<?php else: ?>
    <p>No users found.</p>
<?php endif; ?>
```

## Use `for` when an index is required

```php
<ol>
    <?php for ($i = 0; $i < count($steps); $i++): ?>
        <li><?= htmlspecialchars($steps[$i]) ?></li>
    <?php endfor; ?>
</ol>
```
