# Variables and scope

[← back](../index.md)

ES6 added block-scoped variables.
Use `const` by default and `let` when the value must be reassigned.

## Summary

- [`const`](#const) - declare a value that cannot be reassigned
- [`let`](#let) - declare a block-scoped variable
- [Block scope](#block-scope) - variables live inside `{ ... }`
- [Temporal dead zone](#temporal-dead-zone) - variables cannot be used before declaration

## const

`const` prevents reassignment.

```js
const name = 'Alice';

name = 'Bob';
// TypeError
```

Objects and arrays declared with `const` can still be changed.

```js
const user = { name: 'Alice' };
user.name = 'Bob';
```

## let

Use `let` when the variable is reassigned.

```js
let count = 0;
count += 1;
```

## Block scope

`let` and `const` are visible only inside the current block.

```js
if (true) {
    const message = 'Hello';
}

console.log(message);
// ReferenceError
```

## Temporal dead zone

Unlike `var`, `let` and `const` cannot be used before the declaration line.

```js
console.log(total);
// ReferenceError

const total = 10;
```
