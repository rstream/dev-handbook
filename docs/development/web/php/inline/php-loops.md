# Looping over blocks

[← back](index.md)

Use loops when one HTML fragment must be rendered multiple times.
In templates, `foreach` is the most common choice.

## Summary

- [Render a list with `foreach`](#render-a-list-with-foreach) - repeat markup and escape output with `htmlspecialchars()`
- [Use keys and values](#use-keys-and-values) - render associative arrays with `htmlspecialchars()`
- [Show a fallback when the array is empty](#show-a-fallback-when-the-array-is-empty) - handle empty lists with `if`
- [Use `for` when an index is required](#use-for-when-an-index-is-required) - loop by numeric index with `count()`

## <a id="render-a-list-with-foreach"></a>Render a list with `foreach`

```php
<ul>
    <?php foreach ($users as $user): ?>
        <li><?= htmlspecialchars($user['name']) ?></li>
    <?php endforeach; ?>
</ul>
```

## <a id="use-keys-and-values"></a>Use keys and values

```php
<ul>
    <?php foreach ($prices as $name => $price): ?>
        <li><?= htmlspecialchars($name) ?>: <?= htmlspecialchars((string) $price) ?></li>
    <?php endforeach; ?>
</ul>
```

## <a id="show-a-fallback-when-the-array-is-empty"></a>Show a fallback when the array is empty

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

## <a id="use-for-when-an-index-is-required"></a>Use `for` when an index is required

```php
<ol>
    <?php for ($i = 0; $i < count($steps); $i++): ?>
        <li><?= htmlspecialchars($steps[$i]) ?></li>
    <?php endfor; ?>
</ol>
```
