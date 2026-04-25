# What inline PHP is

[← back](index.md)

Inline PHP means embedding short PHP snippets directly into an HTML template returned by the server.

Typical use cases:
- print variable values
- show or hide HTML blocks
- render repeated blocks from arrays

Keep the template focused on presentation.
Prepare data before including the template whenever possible.

```php
<?php
$pageTitle = 'Products';
$products = ['Keyboard', 'Mouse', 'Monitor'];
?>

<h1><?= htmlspecialchars($pageTitle) ?></h1>
<ul>
    <?php foreach ($products as $product): ?>
        <li><?= htmlspecialchars($product) ?></li>
    <?php endforeach; ?>
</ul>
```
