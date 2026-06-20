# Declaration files

[← back](../index.md)

`.d.ts` files contain only type information. They describe JavaScript code,
globals, generated files, or bundler imports that TypeScript cannot infer from
regular `.ts` / `.tsx` files.

Common use cases:

- typing an untyped JavaScript package;
- describing globals such as `window.appConfig`;
- adding missing fields to existing library types;
- allowing imports of images, CSS modules, and other non-code assets.

Declaration files are usually placed near the code that needs them or in a
separate `types` directory:

```txt
src/
  app.ts
  vite-env.d.ts
types/
  old-library.d.ts
  assets.d.ts
```

## Ambient declarations

Declarations that are not imported from a real TypeScript file are called
ambient declarations. They tell TypeScript: "this value/module exists at
runtime, trust this shape".

```ts
declare const __BUILD_ID__: string;
```

This does not create `__BUILD_ID__` in JavaScript. It only describes a value
that must already exist at runtime.

## Module declaration

```ts
declare module "old-library" {
  export function format(value: string): string;
}
```

Use when a package has no types.

Then TypeScript understands imports from that package:

```ts
import { format } from "old-library";

format("hello");
```

If the library has a default export:

```ts
declare module "legacy-parser" {
  export type ParseOptions = {
    strict?: boolean;
  };

  export default function parse(input: string, options?: ParseOptions): unknown;
}
```

If you do not know the exact shape yet, start narrow enough to be useful instead
of using `any` everywhere:

```ts
declare module "legacy-config" {
  export type Config = Record<string, string | number | boolean>;

  export function loadConfig(path: string): Config;
}
```

Use `unknown` for values that callers must validate before using:

```ts
declare module "legacy-json" {
  export function parse(input: string): unknown;
}
```

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

Without `export {}`, the file is treated as a script. For small global-only
files that can work, but using `export {}` avoids accidental global declarations
and makes the intent clearer.

## Module augmentation

Module augmentation extends types from an existing module. Use it when a library
already has types, but your project adds behavior or the published types are
missing something.

Example: a framework request object receives a `user` field from middleware.

```ts
import type { User } from "../src/auth/user";

declare module "some-server-framework" {
  interface Request {
    user?: User;
  }
}
```

After that, code that imports `Request` from the framework can access the added
field:

```ts
import type { Request } from "some-server-framework";

function getUserId(req: Request): string | undefined {
  return req.user?.id;
}
```

Augmentation works only for declarations that can be merged, most commonly
interfaces. It cannot replace an existing type alias.

## Global augmentation

Global augmentation extends global types such as `Window`, `Document`, or
`NodeJS.ProcessEnv`.

```ts
declare global {
  interface Window {
    analytics?: {
      track(event: string, payload?: Record<string, unknown>): void;
    };
  }
}

export {};
```

Usage:

```ts
window.analytics?.track("page_view", {
  path: location.pathname
});
```

## Asset declarations

Bundlers can import files that TypeScript does not understand by default. A
declaration file describes what such imports return.

For image URLs:

```ts
declare module "*.svg" {
  const src: string;
  export default src;
}

declare module "*.png" {
  const src: string;
  export default src;
}

declare module "*.jpg" {
  const src: string;
  export default src;
}
```

Usage:

```ts
import logoUrl from "./logo.svg";
import avatarUrl from "./avatar.png";

const image = new Image();
image.src = avatarUrl;
```

Some React setups support importing an SVG as a component. The exact declaration
depends on the bundler/plugin. For example:

```ts
declare module "*.svg?react" {
  import type { ComponentType, SVGProps } from "react";

  const Component: ComponentType<SVGProps<SVGSVGElement>>;
  export default Component;
}
```

Usage:

```tsx
import Logo from "./logo.svg?react";

export function Header() {
  return <Logo aria-label="Application logo" />;
}
```

## CSS modules

CSS modules usually compile class names into an object where keys are local class
names and values are generated class names.

```ts
declare module "*.module.css" {
  const classes: Record<string, string>;
  export default classes;
}
```

Usage:

```tsx
import styles from "./Button.module.css";

export function Button() {
  return <button className={styles.primary}>Save</button>;
}
```

For stricter types, generate `.d.ts` files per CSS module:

```ts
// Button.module.css.d.ts
declare const classes: {
  readonly root: string;
  readonly primary: string;
  readonly disabled: string;
};

export default classes;
```

This catches typos such as `styles.primray`.

## Include declarations

Make sure the `.d.ts` file is included by `tsconfig.json`.

```json
{
  "include": ["src", "types"]
}
```

If the declaration file is outside `include`, TypeScript will ignore it. If
`compilerOptions.types` is set, TypeScript includes only the listed global type
packages, so project declarations must still be covered by `include` or `files`.

## Practical rules

- A `.d.ts` file describes runtime behavior; it does not implement it.
- Prefer precise types over `any`.
- Use `unknown` when the value must be checked by the caller.
- Use module declarations for untyped modules.
- Use module augmentation to extend existing library modules.
- Use global augmentation only for real globals.
- Keep asset declarations close to the bundler behavior used by the project.
