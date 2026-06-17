# x-show and x-if

[← back](index.md)

Both directives display content conditionally, but they handle the DOM
differently.

## x-show

`x-show` keeps the element in the DOM and toggles its CSS `display` property:

```html
<div x-data="{ open: false }">
    <button @click="open = !open">Toggle</button>
    <div x-show="open" x-cloak>Content</div>
</div>
```

Use it when the content is toggled frequently. `x-cloak` prevents initially
hidden content from flashing before Alpine starts.

## x-if

`x-if` adds and removes the element from the DOM. It must be placed on a
`<template>` containing one root element:

```html
<div x-data="{ open: false }">
    <template x-if="open">
        <div>Content</div>
    </template>
</div>
```

Use it when the content should not exist in the DOM while the condition is
false. Unlike `x-show`, `x-if` cannot be combined directly with `x-transition`.
