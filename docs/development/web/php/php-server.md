# Running PHP server

[← back](./index.md)

PHP includes a built-in web server for local development.
Check that PHP is installed:

```sh
php --version
```

## Serve the current folder

Run PHP server in the current folder:

```sh
php -S localhost:8080
```

Open `http://localhost:8080/` in a browser.
PHP uses the directory where the command was started as the document root.
For `/`, it normally serves `index.php` or `index.html` when one exists.

## Serve a specific folder

Use the `-t` option to specify the document root:

```sh
php -S localhost:8080 -t public
```

In this example, a request to `http://localhost:8080/index.php` serves
`public/index.php`.

The path may be relative to the current folder or absolute:

```sh
php -S localhost:8080 -t /var/www/example/public
```

You can also change to the required folder before starting the server:

```sh
cd public
php -S localhost:8080
```

## Host and port

The command format is:

```sh
php -S <host>:<port> [-t <document-root>]
```

- `localhost` makes the server available only from the local machine.
- `8080` is the port. Use another free port when `8080` is already in use.
- `0.0.0.0` listens on all network interfaces and may expose the server to
  other devices on the network:

```sh
php -S 0.0.0.0:8080 -t public
```

Press `Ctrl+C` in the terminal to stop the server.

The built-in server is intended for development and testing. Do not use it as
a production web server.
