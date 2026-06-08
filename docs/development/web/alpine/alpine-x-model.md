# x-model

[← back](index.md)

The `x-model` directive creates a two-way binding between a form control and
Alpine state:

```html
<div x-data="{ name: '' }">
    <input x-model="name">
    <span x-text="name"></span>
</div>
```

It works with text inputs, textareas, checkboxes, radio buttons, selects, and
range inputs.

Useful modifiers include:

* `.lazy` - update on the `change` event instead of every input event
* `.debounce` - delay updates while the user is typing
* `.number` - convert the value to a number
* `.boolean` - convert supported values to booleans

```html
<input type="number" x-model.number="quantity">
<input x-model.debounce.500ms="search">
```
