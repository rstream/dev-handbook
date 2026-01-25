# Webpack - basic config

[← back](index.md)

This basic config allows the following:
* JS imports
* CSS imports
* image imports (PNG) - copy images to dest directory
* image imports (GIF) - make images embedded as data-URLs
* create HTML file based on template
* has a dev server
* this config is for a dev (non-minified) mode

Node dependencies to be installed:
* webpack
* webpack-cli
* webpack-dev-server
* html-webpack-plugin
* clean-webpack-plugin
* css-loader
* style-loader

Run to install:
```sh
npm install -D webpack webpack-cli webpack-dev-server html-webpack-plugin clean-webpack-plugin css-loader style-loader
```

```js
import path from "path";
import HtmlWebpackPlugin from "html-webpack-plugin";
import { CleanWebpackPlugin } from "clean-webpack-plugin";

export default {
    resolve: {
        // default extension for import (if extension is omitted)
        extensions: ['.js', '.jsx'],
    },
    // entry root folder
    context: path.resolve('src'),
    // entries
    entry: {
        app: './index.js'
    },
    // output
    output: {
        filename: 'app/[name].js',
        path: path.resolve('dist')
    },
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: [ // styles - fron END to BEGINNING
                    'style-loader', // 2. inject style to <head>
                    'css-loader'    // 1. convert CSS to JS
                ]
            },
            { // file assets (copied)
                test: /\.(jpg|png)$/i,
                type: 'asset/resource',
                generator: {
                    filename: 'assets/[name][ext]'
                }
            },
            { // assets (inline)
                test: /\.gif$/i,
                type: 'asset/inline'
            }
        ]
    },
    plugins: [
        // create HTML based on template
        new HtmlWebpackPlugin({ template: './index-tpl.html', filename: 'index.html'}),
        // clean "dist" folder before writing new files
        new CleanWebpackPlugin()
    ],
    devServer: {
        static: './public',
        port: 3000
    },
    mode: 'development'
};
```