# Common mistakes

[← back](index.md)

## Printing unescaped input

```php
<p><?= $comment ?></p>
```

Prefer:

```php
<p><?= htmlspecialchars($comment) ?></p>
```

## Too much logic in the template

Avoid large condition chains, heavy filtering, or data transformation inside HTML files.

## Database access in the template

Do not query the database from the view layer.
Fetch and prepare the data before rendering.

## Hard-to-read mixed syntax

This is harder to maintain:

```php
<?php foreach ($items as $item) { ?>
    <li><?php echo htmlspecialchars($item); ?></li>
<?php } ?>
```

This is usually clearer:

```php
<?php foreach ($items as $item): ?>
    <li><?= htmlspecialchars($item) ?></li>
<?php endforeach; ?>
```
