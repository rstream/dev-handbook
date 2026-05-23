# Collections

[← back](../index.md)

ES6 added collection types for cases where plain objects and arrays are not ideal.

## Summary

- [`Map`](#map) - key-value collection with any key type
- [`Set`](#set) - collection of unique values
- [`WeakMap`](#weakmap) - object keys without preventing garbage collection
- [`WeakSet`](#weakset) - object set without preventing garbage collection

## Map

Use `Map` when keys are not only strings or when frequent add/remove operations matter.

```js
const usersById = new Map();

usersById.set(10, { name: 'Alice' });
usersById.set(20, { name: 'Bob' });

const user = usersById.get(10);
```

Common methods:

```js
usersById.has(10);
usersById.delete(20);
usersById.size;
```

Iterate entries:

```js
for (const [id, user] of usersById) {
  console.log(id, user.name);
}
```

## Set

`Set` stores unique values.

```js
const roles = new Set();

roles.add('admin');
roles.add('editor');
roles.add('admin');

roles.size;
// 2
```

Remove duplicates from an array:

```js
const uniqueTags = [...new Set(tags)];
```

## WeakMap

`WeakMap` keys must be objects.
It is useful for storing metadata without keeping the object alive.

```js
const state = new WeakMap();

const button = document.querySelector('button');
state.set(button, { clicked: false });
```

Weak collections are not iterable.

## WeakSet

`WeakSet` stores unique object references.

```js
const processed = new WeakSet();

processed.add(user);
processed.has(user);
```
