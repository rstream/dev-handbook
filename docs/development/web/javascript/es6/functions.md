# Functions

[← back](../index.md)

ES6 made function syntax shorter and argument handling cleaner.

## Summary

- [Arrow functions](#arrow-functions) - short function syntax
- [Lexical this](#lexical-this) - arrow functions do not create their own `this`
- [Default parameters](#default-parameters) - fallback argument values
- [Rest parameters](#rest-parameters) - collect extra arguments into an array

## Arrow functions

```js
const double = (value) => {
    return value * 2;
};
```

For one expression, omit `{}` and `return`.

```js
const double = value => value * 2;
```

They are useful with array methods.

```js
const names = users.map(user => user.name);
```

## Lexical this

Arrow functions keep `this` from the surrounding scope.

```js
const timer = {
    seconds: 0,
    start() {
        setInterval(() => {
            this.seconds += 1;
        }, 1000);
    }
};
```

Do not use arrow functions as object methods when the method needs its own `this`.

## Default parameters

```js
function greet(name = 'Guest') {
    return `Hello, ${name}`;
}
```

## Rest parameters

Rest parameters collect arguments into a real array.

```js
function sum(...numbers) {
    return numbers.reduce((total, number) => total + number, 0);
}

sum(1, 2, 3);
// 6
```
