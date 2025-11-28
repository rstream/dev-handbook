# package.json

`package.json` file contains node project settings.
It contains a JSON data with multiple keys.

## type

defines the node project type, can be one of:
* `commonjs` (default) - using "require" for importing dependencies
* `module` - using "import" for importing dependencies

If you set `module`:
```json
{
  "type": "module"
}
```

you should always define the extension of your custm imported module:
```js
import myModule from './my-module.js';
```