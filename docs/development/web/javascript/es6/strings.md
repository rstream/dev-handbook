# Strings

[← back](../index.md)

ES6 added template literals and a few common string checks.

## Summary

- [Template literals](#template-literals) - strings with interpolation
- [Multiline strings](#multiline-strings) - strings across several lines
- [String checks](#string-checks) - `startsWith()`, `endsWith()`, `includes()`
- [Repeat string](#repeat-string) - duplicate a string with `repeat()`

## Template literals

Use backticks and `${...}` for interpolation.

```js
const name = 'Alice';
const message = `Hello, ${name}`;
```

Expressions are allowed.

```js
const total = `Total: ${price * count}`;
```

## Multiline strings

Template literals can span multiple lines.

```js
const html = `
  <section>
    <h1>Profile</h1>
  </section>
`;
```

## String checks

```js
const file = 'photo.jpg';

file.startsWith('photo');
file.endsWith('.jpg');
file.includes('to');
```

## Repeat string

```js
const line = '-'.repeat(20);
```
