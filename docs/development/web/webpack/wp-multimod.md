# Webpack - multiple modules

[← back](index.md)

This example would create 2 output files based on 2 entry points:
* app.build.js
* m2.build.js

```js
export default {
    mode: 'development',
    context: path.resolve('src'), // common part of the path to entry points
    entry: {
        app : './index.js',
        m2: './m2/module-2.js'
    },
    output: {
        filename: '[name].build.js', // output naming template
        path: path.resolve('dist') // path to the final build (should be absolute!)
    }
};
```