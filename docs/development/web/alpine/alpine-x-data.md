# x-data

[← back](index.md)

The `x-data` directive defines an Alpine component and its reactive state.
Properties and methods declared in `x-data` are available to the element and
its descendants:

```html
<div x-data="{ count: 0 }">
    <button @click="count++">Increment</button>
    <span x-text="count"></span>
</div>
```

The state can be declared inline or provided by a reusable component registered
with `Alpine.data`:

```html
<div x-data="counter">
    <button @click="increment()">Increment</button>
    <span x-text="count"></span>
</div>

<script>
    document.addEventListener('alpine:init', () => {
        Alpine.data('counter', () => ({
            count: 0,
            increment() {
                this.count++
            },
        }))
    })
</script>
```

Nested components can read properties from their parent scope unless they
define properties with the same names.
