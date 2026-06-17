# x-for

[← back](index.md)

The `x-for` directive renders an element for every item in a collection. It
must be placed on a `<template>` containing one root element:

```html
<ul x-data="{ users: [{ id: 1, name: 'Ada' }] }">
    <template x-for="user in users" :key="user.id">
        <li x-text="user.name"></li>
    </template>
</ul>
```

Use `:key` with a stable unique value when items can be added, removed, or
reordered. This allows Alpine to associate each DOM element with the correct
item.

The current index is available as a second expression variable:

```html
<template x-for="(user, index) in users" :key="user.id">
    <div>
        <span x-text="index"></span>
        <span x-text="user.name"></span>
    </div>
</template>
```
