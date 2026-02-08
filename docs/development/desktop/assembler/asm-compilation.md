# Assembler file compilation

[← back](index.md)

Compilation goes in 2 phases:
* compiling
* linking

## Compile

Compile with a model specified in the *.asm file (or small by default):
```sh
tasm myapp.asm
```
Compile with a tiny model (for *.com files):
```sh
tasm /t myapp.asm
```

The output would be an `object file` (*.obj).

## Link

Link object file into an executable (*.com / *.exe) with tiny model:
```sh
tlink /t myapp.obj
```
>Note: model specifier (/t) should always be set

## Dos Navigator

Very convenient way to go is to use DN (Dos Navigator).  
It has the following features:
* Text editor with syntax highlight (F4)
* Compile+link *.asm files just with pressing `Enter` key