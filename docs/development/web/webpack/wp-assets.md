# Webpack - assets

[← back](index.md)

Working with assets (icons, images, sounds, fonts, other files)

Asset's type can be:
* `asset/source` - use content of the file as a string value
* `asset/resource` - copy files to the destination folder
* `asset/inline` - embedded into JS file as a data-URL
* `asset` - auto choose (by size): `resource` vs `inline`  (limit in bytes can be set; default = `8192`)

```js
export default {
    output: {
        filename: 'app.js',
        path: path.resolve('dist'),
        assetModuleFilename: 'assets/[name][ext]'
    },
    module: {
        rules: [
            { // JPG/PNG - copy as files
                test: /\.(jpg|png)$/i,
                type: 'asset/resource'
            },
            { // TXT - use content as string
                test: /\.txt$/i,
                type: 'asset/source'
            },
            { // GIF - make inline
                test: /\.gif$/i,
                type: 'asset/inline'
            },
            { // WebP - make inline if not bigger than 2048 bytes (otherwise - copy as files)
                test: /\.webp$/i,
                type: 'asset', // auto !
                parser: {
                    dataUrlCondition: {
                        maxSize: 2048
                    }
                }
            },
            { // DATA - copy as files and to special folder
                test: /\.dat$/i,
                type: 'asset/resource',
                generator: { // overrides assetModuleFilename !
                    filename: 'data/[name][ext]'
                }
            }
        ]
    }
};
```