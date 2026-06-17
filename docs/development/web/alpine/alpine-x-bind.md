# x-bind

[← back](index.md)

The `x-bind` directive sets an HTML attribute from an Alpine expression:

```html
<button x-data="{ disabled: true }" x-bind:disabled="disabled">
    Submit
</button>
```

The shorthand syntax is `:`:

```html
<a x-data="{ url: '/profile' }" :href="url">Profile</a>
```

It is commonly used to bind classes:

```html
<div
    x-data="{ active: false }"
    :class="{ 'is-active': active }"
></div>
```

For boolean attributes such as `disabled`, `checked`, and `required`, Alpine
adds or removes the attribute according to the expression's value.
