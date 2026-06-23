# VS Code setup for Assembler

[← back](../index.md)

## Install MASM/TASM extension

Install the MASM/TASM extension for VS Code:
https://marketplace.visualstudio.com/items?itemName=xsro.masm-tasm

More details:
https://github.com/dosasm/masm-tasm

This will give:
* syntax highlight
* compilation/running
* debugging

## Commands

After right click in the code editor (any place) you would have additional options in context menu:
* `Open Emulator` - opens emulator where your file would be available as `test.asm`
* `Run ASM code` - open emulator and run
* `Debug ASM code` - open emulator and run id debug mode

## Configs

Config allows to override default commands (shown in the context menu).  
This is useful for `model-tiny` programs, since by default linker will produce an `*.exe` file, and it would not work properly.

> Note: Configs must be stored to `.vscode/settins.json`

### Config for model tiny

Use this config to make the extension produce `*.com` files.

```json
{
    "masmtasm.ASM.actions": {
        "TASM-com": {
            "baseBundle": "<built-in>/TASM.jsdos",
            "before": [
                "PATH %PATH%;C:\\TASM"
            ],
            "run": [
                "TASM ${file}",
                "TLINK /t ${filename}",
                "${filename}"
            ],
            "debug": [
                "TASM /zi ${file}",
                "TLINK /t/v/3 ${filename}.obj",
                "TD ${filename}.exe"
            ]
        }
    },
    "masmtasm.ASM.assembler": "TASM-com"
}
```
