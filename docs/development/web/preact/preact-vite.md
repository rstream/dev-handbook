# Preact + Vite

[← back](index.md)

## Installation

Install `create-vite` (scaffolding tool) globally:
```sh
npm i -g create-vite
```

## Create preact template

Create a preact javascript template (JSX):
```sh
create-vite myTestProject --template preact
```

Create a preact typescript template (TSX):
```sh
create-vite myTestProject --template preact-ts
```

## Building and running local server

### Build the preact app
```sh
npm run build
```
The compiled app would be in the `dist` folder.

### Run the preact app on local server
```sh
npm run dev
```
To access local server open the URL: `http://localhost:5173/`