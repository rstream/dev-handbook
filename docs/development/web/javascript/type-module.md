# <script type=\"module\">

[← back](index.md)

## What happens when you add script as a `module` ?
```html
<script type="module" src="app.js"></script>
```
### Strict mode ON

As if you are using 
```js
use strict;
```

### Always defer

Script would be executed after DOM rendering is completed, as if you are using `defer`:
```html
<script type="module" src="app.js" defer></script>
```

### Must add extensions to your modules

Correct:
```js
import './utils.js';
```
Wrong:
```js
import './utils';
```

### Top-level await

You can use await on the top level (not only inside async functions)

### Undefined "this"

**this** is `undefined` (not `window`).

### Global variables are not in "window"

All globally defined variable are not available in `window` object.