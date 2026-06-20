# Declaration files

[← back](../index.md)

`.d.ts` files describe types for existing JavaScript or globals.

## Module declaration

```ts
declare module "old-library" {
  export function format(value: string): string;
}
```

Use when a package has no types.

## Global declaration

```ts
declare global {
  interface Window {
    appConfig: {
      apiUrl: string;
    };
  }
}

export {};
```

`export {}` makes the file a module while still allowing global augmentation.

## Asset declarations

```ts
declare module "*.svg" {
  const src: string;
  export default src;
}
```

Useful when importing assets through a bundler.

## Include declarations

Make sure the `.d.ts` file is included by `tsconfig.json`.

```json
{
  "include": ["src", "types"]
}
```
