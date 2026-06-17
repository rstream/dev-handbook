# x-text and x-html

[← back](index.md)

Use `x-text` to set an element's text content from an Alpine expression:

```html
<span x-data="{ name: 'Ada' }" x-text="name"></span>
```

The value is escaped and rendered as plain text. This should be the default
choice for displaying dynamic content.

Use `x-html` only when the value contains HTML that must be rendered:

```html
<div x-data="{ content: '<strong>Hello</strong>' }" x-html="content"></div>
```

Never pass untrusted or user-provided content to `x-html`: it writes to
`innerHTML` and can introduce an XSS vulnerability.
