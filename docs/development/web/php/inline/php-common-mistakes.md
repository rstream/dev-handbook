# Common mistakes

[← back](index.md)

## Summary

- [Printing unescaped input](#printing-unescaped-input) - `htmlspecialchars()` escapes dynamic values
- [Too much logic in the template](#too-much-logic-in-the-template) - keep complex work outside HTML
- [Database access in the template](#database-access-in-the-template) - query before rendering
- [Hard-to-read mixed syntax](#hard-to-read-mixed-syntax) - prefer alternative template syntax

## <a id="printing-unescaped-input"></a>Printing unescaped input

```php
<p><?= $comment ?></p>
```

Prefer:

```php
<p><?= htmlspecialchars($comment) ?></p>
```

## <a id="too-much-logic-in-the-template"></a>Too much logic in the template

Avoid large condition chains, heavy filtering, or data transformation inside HTML files.

## <a id="database-access-in-the-template"></a>Database access in the template

Do not query the database from the view layer.
Fetch and prepare the data before rendering.

## <a id="hard-to-read-mixed-syntax"></a>Hard-to-read mixed syntax

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
