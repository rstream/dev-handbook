# Outputting values

[← back](index.md)

Use `<?= ... ?>` to insert a PHP expression into HTML.

## Print text content

```php
<h1><?= htmlspecialchars($title) ?></h1>
<p><?= htmlspecialchars($description) ?></p>
```

## Print attribute values

```php
<img src="<?= htmlspecialchars($imageUrl) ?>" alt="<?= htmlspecialchars($imageAlt) ?>">
```

## Provide a fallback value

```php
<p><?= htmlspecialchars($nickname ?? 'Guest') ?></p>
```

Prefer `<?= ... ?>` over `<?php echo ...; ?>` for simple output inside templates.
