# package.json

[← back](index.md)

`package.json` contains Node.js project metadata, scripts, and dependency lists.

## Summary

- [Create package.json](#create-package-json) - initialize a Node.js project
- [Install dependencies](#install-dependencies) - install modules from npm
- [dependencies](#dependencies) - packages needed by the app at runtime
- [devDependencies](#devdependencies) - packages needed only for development
- [Remove a dependency](#remove-a-dependency) - uninstall a package
- [scripts](#scripts) - project commands
- [type](#type) - choose ES modules
- [package-lock.json](#package-lock-json) - exact installed dependency versions
- [node_modules](#node-modules) - installed package files

## Create package.json

Create a `package.json` file interactively:

```bash
npm init
```

Create it with default answers:

```bash
npm init -y
```

## Install dependencies

Install all packages listed in `package.json`:

```bash
npm install
```

Short form:

```bash
npm i
```

Install and add a package to `dependencies`:

```bash
npm install lodash
```

Short form:

```bash
npm i lodash
```

Install and add a package to `devDependencies`:

```bash
npm install eslint --save-dev
```

Short form:

```bash
npm i eslint -D
```

## dependencies

`dependencies` are packages needed to run the application.

Example:

```json
{
    "dependencies": {
        "express": "^5.1.0"
    }
}
```

Use this for runtime libraries: web servers, database clients, UI libraries, helpers used by production code.

## devDependencies

`devDependencies` are packages needed only while developing, testing, or building the project.

Example:

```json
{
    "devDependencies": {
        "eslint": "^9.0.0",
        "vite": "^6.0.0"
    }
}
```

Use this for linters, test runners, bundlers, formatters, and TypeScript.

## Remove a dependency

Remove a package from `package.json` and `node_modules`:

```bash
npm uninstall lodash
```

Short form:

```bash
npm rm lodash
```

## scripts

`scripts` are named commands for the project.

Example:

```json
{
    "scripts": {
        "dev": "vite",
        "test": "vitest",
        "start": "node server.js"
    }
}
```

Run a script:

```bash
npm run dev
```

Some script names have shortcuts:

```bash
npm start
npm test
```

## type

Defines the Node.js module type.

Use `"module"` for ES modules:

```json
{
    "type": "module"
}
```

```js
import fs from 'node:fs';
```

When using `"type": "module"`, local imports usually need file extensions:

```js
import myModule from './my-module.js';
```

## package-lock.json

`package-lock.json` stores the exact versions installed by npm.

Commit it to the repository for applications so other developers and deployment systems install the same dependency tree.

## node_modules

`node_modules` contains installed package files.

Do not commit it to the repository. It can be recreated with:

```bash
npm install
```
