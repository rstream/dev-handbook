# TypeScript packages

[← back](../index.md)

Install the working minimum as dev dependencies:

```sh
npm install -D typescript @types/node
```

- `typescript` provides the `tsc` compiler, type checker, and standard TypeScript tooling.
- `@types/node` provides types for Node.js APIs used by config files, build scripts, and CLI tooling.

Browser APIs such as `document`, `window`, and DOM events are typed by TypeScript itself when the project includes DOM libs in `tsconfig.json`.
