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

## Visibility

```ts
class User {
  public name: string;
  private token: string;
  protected role: string;
}
```

Note: `private` and `protected` are TypeScript checks. Use JS `#field` for runtime privacy.

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

```ts
abstract class Store {
  abstract save(): void;
}
```
