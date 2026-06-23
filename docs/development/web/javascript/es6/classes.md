# Classes

[← back](../index.md)

Classes are syntax over JavaScript prototypes.
Use them when objects share behavior and need clear construction.

## Summary

- [Define a class](#define-a-class) - `class` and `constructor`
- [Methods](#methods) - functions on class instances
- [Inheritance](#inheritance) - `extends` and `super`
- [Static methods](#static-methods) - methods on the class itself

## Define a class

```js
class User {
    constructor(name) {
        this.name = name;
    }
}

const user = new User('Alice');
```

## Methods

```js
class User {
    constructor(name) {
        this.name = name;
    }

    greet() {
        return `Hello, ${this.name}`;
    }
}
```

Methods are shared through the prototype.

## Inheritance

Use `extends` to create a subclass.
Use `super()` before accessing `this` in a child constructor.

```js
class Admin extends User {
    constructor(name, permissions) {
        super(name);
        this.permissions = permissions;
    }

    can(permission) {
        return this.permissions.includes(permission);
    }
}
```

## Static methods

Static methods are called on the class, not on an instance.

```js
class User {
    static fromJSON(data) {
        return new User(data.name);
    }
}

const user = User.fromJSON({ name: 'Alice' });
```
