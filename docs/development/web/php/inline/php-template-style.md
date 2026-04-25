# Recommended template style

[← back](index.md)

Use a consistent style so mixed HTML/PHP templates stay readable.

## Recommended rules

- use `<?= ... ?>` for output
- use `if: endif;` and `foreach: endforeach;` for HTML blocks
- escape dynamic output by default
- keep business logic outside the template
- keep indentation aligned with the surrounding HTML

## Example

```php
<section class="products">
    <h2><?= htmlspecialchars($title) ?></h2>

    <?php if ($products): ?>
        <ul>
            <?php foreach ($products as $product): ?>
                <li><?= htmlspecialchars($product['name']) ?></li>
            <?php endforeach; ?>
        </ul>
    <?php else: ?>
        <p>No products available.</p>
    <?php endif; ?>
</section>
```
