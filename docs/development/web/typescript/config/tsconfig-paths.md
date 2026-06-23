# Paths

[← back](../index.md)

`paths` creates compile-time import aliases.

## Alias config

```json
{
    "compilerOptions": {
        "baseUrl": ".",
        "paths": {
            "@/*": ["src/*"],
            "@components/*": ["src/components/*"]
        }
    }
}
```

## Usage

```ts
import { Button } from "@/components/Button";
```

## Runtime caveat

TypeScript does not rewrite these imports by itself.

Your bundler, test runner, or Node runtime must understand the same alias.

- Vite: `resolve.alias`
- Webpack: `resolve.alias`
- Jest/Vitest: test resolver config
- Node: custom loader, package imports, or avoid TS-only aliases
