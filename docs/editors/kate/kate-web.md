# Kate for Web development

[← back](../index.md)

Set up Kate for web development.  
Kate uses LSP to understand languages.

## Typescript/Javascript

Install typescript/javascript LSP

```sh
npm install -g typescript typescript-language-server
```

## HTML/CSS

Install VS Code langservers (yes, they will be used by Kate):

```sh
npm install -g vscode-langservers-extracted
```

package includes:
* `vscode-html-language-server`
* `vscode-css-language-server`
* `vscode-json-language-server`
* `vscode-eslint-language-server`

But Kate will look for these (written together!):
* `vscode-html-languageserver`
* `vscode-json-languageserver`

So you have to create symlinks:

```sh
sudo ln -s "$(which vscode-html-language-server)" /usr/local/bin/vscode-html-languageserver
```
```sh
sudo ln -s "$(which vscode-json-language-server)" /usr/local/bin/vscode-json-languageserver
```
