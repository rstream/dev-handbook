# Webpack - loading styles

[← back](index.md)

There are 2 general approaches to work with styles:
* style-loader - embed CSS into JS
* MiniCssExtractPlugin - keep CSS as separate files

## style-loader

Embeds styles into the JS file.

Good for development:
* extra simple - everything inside a single JS file
* fast compile
* fast HMR

Prerequisites:
```sh
npm install -D css-loader style-loader
```

```js
import path from 'path';

export default {
    context: path.resolve('src'),
    entry: {        
        app: './index'
    },
    output: {
        filename: 'app.js',
        path: path.resolve('dist')
    },
    module: {
		rules: [
			{
				test: /\.css$/i,
				use: ['style-loader', 'css-loader'],
			}
		]
	}
};
```

## MiniCssExtractPlugin

Creates separate CSS files. Number of files == number of chunks (chunk is an entry or a dynamic JS import).

Good for production:
* styles are loaded before JS code run (no flickering)
* styles are cached by browser

Prerequisites:
```sh
npm install -D css-loader mini-css-extract-plugin
```

```js
import path from 'path';
import MiniCssExtractPlugin from 'mini-css-extract-plugin';

export default {
    context: path.resolve('src'),
    entry: {        
        app: './index'
    },
    output: {
        filename: '[name].js', // app.js
        path: path.resolve('dist')
    },
    plugins: [new MiniCssExtractPlugin({ filename: '[name]-styles.css' })],
    module: {
		rules: [
			{
				test: /\.css$/i,
				use: [MiniCssExtractPlugin.loader, 'css-loader'],
			}
		]
	}
};
```