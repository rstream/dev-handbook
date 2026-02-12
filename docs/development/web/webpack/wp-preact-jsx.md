# Webpack - config for Preact

[← back](index.md)

To make Webpack understand `*.jsx` files use `babel-loader` with the following config (`.babelrc`):

```json
{
    "presets": [
        [
            "@babel/preset-react",
            {
                "runtime": "automatic",
                "importSource": "preact"
            }
        ]
    ]
}
```

Dependencies to be installed:
* `@babel/core`
* `@babel/preset-react`
* `babel-loader`
 
Then use `babel-loader` in the `rules` section for `*.jsx` files:

```js
import path from 'path';
import HtmlWebpackPlugin from 'html-webpack-plugin';
import MiniCssExtractPlugin from 'mini-css-extract-plugin';
import { CleanWebpackPlugin } from 'clean-webpack-plugin';

export default {
    entry: './src/index.jsx',
    output: {
        path: path.resolve('dist'), // absolute path !
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.jsx$/,
                exclude: /node_modules/,
                use: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: [ MiniCssExtractPlugin.loader, 'css-loader']
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            filename: 'index.html',
            template: path.resolve('src/index-tpl.html')
        }),
        new MiniCssExtractPlugin({
            filename: 'style.css'
        }),
        new CleanWebpackPlugin()
    ],
    devServer: {
        static: './public',
        port: 3000
    },
    mode: 'development'
};
```