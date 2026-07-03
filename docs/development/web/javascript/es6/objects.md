# Objects

[← back](../index.md)

ES6 added shorter object syntax and easier ways to extract values.

## Summary

- [Property shorthand](#property-shorthand) - use variable names as property names
- [Method shorthand](#method-shorthand) - shorter object methods
- [Computed property names](#computed-property-names) - dynamic keys
- [Destructuring](#destructuring) - extract object and array values
- [`Object.assign()`](#objectassign) - copy and merge object properties
- [`Object.entries()`](#objectentries) - convert an object to key-value pairs
- [`Object.fromEntries()`](#objectfromentries) - convert key-value pairs to an object

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

## Object.entries

`Object.entries()` returns an array of `[key, value]` pairs.

```js
const user = {
    name: 'Alice',
    role: 'admin'
};

const entries = Object.entries(user);
// [['name', 'Alice'], ['role', 'admin']]
```

It is useful when you need to iterate over both keys and values.

```js
for (const [key, value] of Object.entries(user)) {
    console.log(`${key}: ${value}`);
}
```

## Object.fromEntries

`Object.fromEntries()` creates an object from key-value pairs.

```js
const entries = [
    ['name', 'Alice'],
    ['role', 'admin']
];

const user = Object.fromEntries(entries);
// { name: 'Alice', role: 'admin' }
```

It works well with transformations.

```js
const prices = {
    apple: 1,
    banana: 2
};

const doubled = Object.fromEntries(
    Object.entries(prices).map(([name, price]) => [name, price * 2])
);

// { apple: 2, banana: 4 }
```
