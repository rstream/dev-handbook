# Arrays and iteration

[← back](../index.md)

ES6 added useful array helpers and a clean way to iterate values.

## Summary

- [`for...of`](#forof) - loop over values
- [Array spread](#array-spread) - copy and combine arrays
- [`find()`](#find) - get the first matching item
- [`findIndex()`](#findindex) - get the first matching index
- [`Array.from()`](#arrayfrom) - convert iterable or array-like values
- [`Array.of()`](#arrayof) - create an array from arguments

## for...of

Use `for...of` when you need values from an iterable.

```js
const colors = ['red', 'green', 'blue'];

for (const color of colors) {
  console.log(color);
}
```

Use `for...in` for object keys, not array values.

## Array spread

```js
const first = [1, 2];
const second = [3, 4];

const all = [...first, ...second];
```

Copy an array:

```js
const copy = [...items];
```

## find

`find()` returns the first matching item or `undefined`.

```js
const user = users.find(user => user.id === 10);
```

## findIndex

`findIndex()` returns the first matching index or `-1`.

```js
const index = users.findIndex(user => user.id === 10);
```

## Array.from

`Array.from()` converts iterable or array-like values to arrays.

```js
const letters = Array.from('abc');
// ['a', 'b', 'c']
```

In browser code, it is useful with DOM collections.

```js
const buttons = Array.from(document.querySelectorAll('button'));
```

## Array.of

`Array.of()` creates an array from arguments.

```js
const numbers = Array.of(1, 2, 3);
```
