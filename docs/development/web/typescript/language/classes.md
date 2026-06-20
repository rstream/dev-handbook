# Classes

[← back](../index.md)

TypeScript adds type checking and visibility modifiers to JS classes.

## Fields and constructor

```ts
class User {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

## Parameter properties

```ts
class User {
  constructor(public id: number, private name: string) {}
}
```

This creates and assigns fields automatically.

Same as:

```ts
class User {
  public id: number;
  private name: string;

  constructor(id: number, name: string) {
    this.id = id;
    this.name = name;
  }
}
```

You can use `public`, `private`, `protected`, and `readonly` in constructor params.  
This would create object properties with the same names.

```ts
class User {
  constructor(
    public readonly id: number,
    public name: string,
    private token: string
  ) {}
}

const user = new User(1, "Ann", "secret");

user.id; // ok
user.name = "Bob"; // ok
user.id = 2; // error: readonly
user.token; // error: private
```

## Visibility

```ts
class User {
  public name: string;
  private token: string;
  protected role: string;
}
```

Note: `private` and `protected` are TypeScript checks. Use JS `#field` for runtime privacy.

## Definite assignment

If a field is initialized later, use `!` to tell TypeScript it will be assigned before use.

```ts
class UserForm {
  input!: HTMLInputElement;

  mount(root: HTMLElement) {
    this.input = root.querySelector("input") as HTMLInputElement;
  }
}
```

Use this only when initialization is guaranteed.

## Override

`override` makes TypeScript check that a parent method really exists (error if parent class does not have `render` method).

```ts
class BaseView {
  render() {}
}

class UserView extends BaseView {
  override render() {}
}
```

With `noImplicitOverride`, overriding methods must use `override`.

## Implements

```ts
interface Printable {
  print(): void;
}

class Invoice implements Printable {
  print() {
	  console.log("Printing Invoice...");
  }
}

function print(document: Printable) {
	document.print();
}
```

## Abstract class

Abstract class is a template for further extending. You cannot create objects from an abstract class.
```ts
abstract class Store {
  constructor(protected name: string) {}

  abstract save(): void;

  log() {
    console.log(`Saving ${this.name}`);
  }
}
```

Abstract classes can contain real code and abstract members.

### Extending example 1 (using abstract class constructor)

```ts
class FileStore extends Store {
  save() {
    this.log();
    console.log("Saved to file");
  }
}

const store = new FileStore("users");
store.save();
```

### Extending example 2 (having own constructor)  
If the child class has its own constructor, it must call `super()` before using `this`.

```ts
class DatabaseStore extends Store {
  constructor(name: string, private table: string) {
    super(name);
  }

  save() {
    this.log();
    console.log(`Saved to ${this.table}`);
  }
}

const dbStore = new DatabaseStore("users", "user_table");
dbStore.save();
```

