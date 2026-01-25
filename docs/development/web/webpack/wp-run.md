# Webpack - running tasks

[← back](index.md)

## Build

Run build in default mode (specified in `webpack.config.js`):
```sh
webpack
```

Run build in dev mode:
```sh
webpack --mode development
```

Run build in production mode:
```sh
webpack --mode production
```

## Watch

Run watch & build:
```sh
webpack --watch
```

## Local server

Run local server (server setting are in `webpack.config.js`):
```sh
webpack serve
```

## Set npm tasks

You can set up shortcuts in `package.json`:
```json
{
  "scripts": {
    "build": "webpack --mode development",
    "prod": "webpack --mode production",
    "dev": "webpack serve"
  }
}
```