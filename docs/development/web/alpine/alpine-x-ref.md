# x-ref and $refs

[← back](index.md)

The `x-ref` directive gives a DOM element a local name inside an Alpine
component. You can access the element through the `$refs` magic object:

```html
<div x-data>
    <input x-ref="nameInput">

    <button @click="$refs.nameInput.focus()">Focus input</button>
</div>
```

Use `x-ref` when you need direct access to a real DOM element. Common examples
are focusing an input, reading layout values, controlling media elements, or
passing an element to a third-party library.

## Ref scope

Refs belong to the current Alpine component. A parent component can access refs
declared inside its own `x-data` scope:

```html
<div x-data="{ play() { this.$refs.video.play() } }">
    <video x-ref="video" src="/intro.mp4"></video>

    <button @click="play()">Play</button>
</div>
```

If you create a nested component with another `x-data`, it gets its own refs
scope:

```html
<div x-data>
    <input x-ref="outerInput">

    <div x-data>
        <input x-ref="innerInput">
    </div>
</div>
```

The outer component should not rely on refs from the inner component. Pass data
or dispatch events between components instead.

## After rendering

If the referenced element appears after a state change, wait until Alpine has
updated the DOM with `$nextTick`:

```html
<div x-data="{ editing: false }">
    <button
        @click="
            editing = true;
            $nextTick(() => $refs.title.focus());
        "
    >
        Edit
    </button>

    <input x-show="editing" x-ref="title">
</div>
```

## Reading element values

Prefer `x-model` for normal form state. Use `$refs` only when you specifically
need the element object:

```html
<div x-data="{ width: 0 }">
    <div x-ref="panel">Content</div>

    <button @click="width = $refs.panel.offsetWidth">
        Measure
    </button>

    <span x-text="width"></span>
</div>
```

## Caveats

* `x-ref` names should be static and unique inside one component.
* `$refs.someName` exists only after the element has been rendered.
* For lists rendered with `x-for`, avoid depending on one repeated ref name.
  Store data in state, or use event handlers on each repeated element.
