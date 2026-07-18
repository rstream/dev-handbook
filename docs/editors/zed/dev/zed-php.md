# Zed setup for PHP

[← back](../index.md)

## Install extension

Install PHP extension: `PHP` by Piotr Osiewicz.

## Switch PHP language server to Intelephense

Intelephense gives you HTML autocompletion in `*.php` files (default language server, phpactor, cannot do it).

Add this to your `settings.json`:
```json
{
  "languages": {
      "PHP": {
          "language_servers": [
            "intelephense",
            "!phpactor",
            "!phptools",
            "..."
          ]
      }
    }
}
```

This config enables Intelephense language server, and disables phpactor/phptools.

## Install php8-phar

Only if you are planning to use default language server (phpactor) and `php8-phar` is not installed.

### Linux

By default, PHP Zed extension is using `phpactor` language server, it is distributed as a `phar` file. So it will fail to start if you don't have `php8-phar` installed.
```bash
sudo zypper install php8-phar
```
