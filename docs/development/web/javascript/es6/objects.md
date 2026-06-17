# Objects

[← back](../index.md)

ES6 added shorter object syntax and easier ways to extract values.

## Summary

- [Property shorthand](#property-shorthand) - use variable names as property names
- [Method shorthand](#method-shorthand) - shorter object methods
- [Computed property names](#computed-property-names) - dynamic keys
- [Destructuring](#destructuring) - extract object and array values
- [`Object.assign()`](#objectassign) - copy and merge object properties

## Property shorthand

```js
const name = 'Alice';
const age = 30;

const user = { name, age };
```

## Method shorthand

```js
const user = {
  name: 'Alice',
  greet() {
    return `Hello, ${this.name}`;
  }
};
```

## Computed property names

```js
const field = 'email';

const user = {
  [field]: 'alice@example.com'
};
```

## Destructuring

Object destructuring:

```js
const user = {
  name: 'Alice',
  email: 'alice@example.com'
};

const { name, email } = user;
```

Array destructuring:

```js
const point = [10, 20];
const [x, y] = point;
```

Use defaults when a value may be missing.

```js
const { role = 'viewer' } = user;
```

## Object.assign

`Object.assign()` copies properties into the first object.

```js
const user = { name: 'Alice', role: 'viewer' };
const admin = Object.assign({}, user, { role: 'admin' });
```

Later properties override earlier ones.
