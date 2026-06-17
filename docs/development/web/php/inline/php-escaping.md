# Escaping output

[← back](index.md)

Escape dynamic values before inserting them into HTML to reduce XSS risk.

## Summary

- [Use `htmlspecialchars()` by default](#use-htmlspecialchars-by-default) - escape text content
- [Escape attributes too](#escape-attributes-too) - `htmlspecialchars()` also escapes values inside HTML attributes
- [Avoid raw HTML unless content is trusted](#avoid-raw-html-unless-content-is-trusted) - avoid printing untrusted HTML directly

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
