# x-on and events

[← back](index.md)

The `x-on` directive runs an Alpine expression when a DOM event occurs:

```html
<div x-data="{ open: false }">
    <button x-on:click="open = true">Open</button>
</div>
```

`@` is shorthand for `x-on:`. These declarations are equivalent:

```html
<div x-data="{ save() { /* ... */ } }">
    <button x-on:click="save()">Save</button>
    <button @click="save()">Save</button>
</div>
```

The event is available as `$event`:

```html
<div x-data="{ value: '' }">
    <input @input="value = $event.target.value">
</div>
```

## Event modifiers

Modifiers change how or where an event is handled:

```html
<div x-data="component">
    <form @submit.prevent="save()"></form>
    <button @click.stop="select()"></button>
    <button @click.once="initialize()"></button>
    <input @input.debounce.300ms="search()">
    <div @click.outside="open = false"></div>
    <div @keyup.escape.window="open = false"></div>
</div>
```

Common modifiers:

* `.prevent` - call `preventDefault()`
* `.stop` - stop event propagation
* `.once` - handle the event only once
* `.debounce` and `.throttle` - limit how often the handler runs
* `.outside` - handle clicks outside the element
* `.window` and `.document` - listen on a global event target
* `.enter`, `.escape`, and other key names - filter keyboard events

## Custom events

Dispatch a custom event with `$dispatch` and listen for it using `@`:

```html
<div x-data="component">
    <button @click="$dispatch('saved', { id: 1 })">Save</button>
    <div @saved.window="showNotification($event.detail)"></div>
</div>
```
