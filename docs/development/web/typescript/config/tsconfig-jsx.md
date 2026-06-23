# JSX

[← back](../index.md)

JSX settings are needed for `.tsx` files.

## React-style JSX

```json
{
    "compilerOptions": {
        "jsx": "react-jsx"
    }
}
```

Use for modern React and compatible libraries.

## Preact

```json
{
    "compilerOptions": {
        "jsx": "react-jsx",
        "jsxImportSource": "preact"
    }
}
```

This tells TypeScript where JSX runtime and JSX types come from.

## Preserve JSX

```json
{
    "compilerOptions": {
        "jsx": "preserve"
    }
}
```

Use when another tool transforms JSX.

## Component typing

```tsx
type Props = {
    title: string;
};

export function Card({ title }: Props) {
    return <h2>{title}</h2>;
}
```
