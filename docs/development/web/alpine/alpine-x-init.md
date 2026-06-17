# x-init

[← back](index.md)

The `x-init` directive runs a JavaScript expression when Alpine initializes an
element. It is useful for one-time setup, such as loading data, setting initial
state, or starting a third-party library.

The expression has access to the current `x-data` scope:

```html
<div
    x-data="{ posts: [] }"
    x-init="posts = await (await fetch('/posts')).json()"
></div>
```

`x-init` can also be used on an element without `x-data`. To run code after
Alpine has finished rendering the current DOM updates, use `$nextTick`:

```html
<div x-init="$nextTick(() => console.log('Rendered'))"></div>
```

## `init` method caveat

The `init` method (of the object referenced by `x-data`) is called automatically!

So if you also put it in `x-init` - it will run **TWICE!**
This snippet:

```html
<div x-data="app" x-init="init()"></div>
```

Will run `app.init()` two times:

* first time because Alpine automatically calls methods named `init`
* second time because it is referenced in `x-init`
