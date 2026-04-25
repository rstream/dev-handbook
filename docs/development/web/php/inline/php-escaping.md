# Escaping output

[← back](index.md)

Escape dynamic values before inserting them into HTML to reduce XSS risk.

## Use `htmlspecialchars()` by default

```php
<p><?= htmlspecialchars($message) ?></p>
```

A common explicit form is:

```php
<p><?= htmlspecialchars($message, ENT_QUOTES, 'UTF-8') ?></p>
```

## Escape attributes too

```php
<a href="<?= htmlspecialchars($url, ENT_QUOTES, 'UTF-8') ?>">
    <?= htmlspecialchars($label, ENT_QUOTES, 'UTF-8') ?>
</a>
```

## Avoid raw HTML unless content is trusted

```php
<div><?= $unsafeHtml ?></div>
```

The example above is risky if `$unsafeHtml` contains untrusted input.
