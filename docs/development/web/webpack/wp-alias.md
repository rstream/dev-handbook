# Webpack - aliases

[← back](index.md)

Aliases can be used to get rid of long paths in imports.

`webpack.config.js` (part):
```js
export default {
    resolve: {
        alias: {
            '@assets': path.resolve('src/assets'),
            '@data': path.resolve('src/data')
        }
    }
}
```

Usage in JS module:
```js
import img_formula from "@assets/formula.gif";
import base from '@data/base.dat';
```