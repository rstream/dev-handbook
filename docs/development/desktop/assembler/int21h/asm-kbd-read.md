# Read from keyboard

[← back](../index.md)

## Read a single char from keyboard

```asm
mov		ah, 01h
int		21h
```

The char would be put to `AL`.