# Registers

[← back](../index.md)

Register is a small CPU storage cell.

In 16-bit DOS programs registers usually store:
* values
* addresses
* counters
* interrupt function numbers
* interrupt arguments

## General purpose registers

| Register | Parts | Common use |
|---|---|---|
| `AX` | `AH`, `AL` | accumulator, arithmetic, interrupt function/result |
| `BX` | `BH`, `BL` | base address |
| `CX` | `CH`, `CL` | counter |
| `DX` | `DH`, `DL` | data, interrupt argument/result |

`AX` - accumulator, often used for arithmetic and DOS interrupt function numbers/results.  
`BX` - base register, often used to store a memory address.  
`CX` - counter register, often used in loops and repeated operations.  
`DX` - data register, often used with `AX` or as an argument/result for DOS interrupts.

Each register is 16-bit:

```asm
mov ax, 1234h
```

High and low bytes can be accessed separately:

```asm
mov ah, 09h      ; high byte of AX
mov al, 41h      ; low byte of AX
```

## Index and pointer registers

| Register | Common use |
|---|---|
| `SI` | source index |
| `DI` | destination index |
| `BP` | stack frame / base pointer |
| `SP` | stack pointer |

`SI` - source index, usually points to the source data when reading from memory.  
`DI` - destination index, usually points to the destination memory when writing or copying data.  
`BP` - base pointer, usually points to data inside the current stack frame.  
`SP` - stack pointer, points to the current top of the stack.

Example:

```asm
mov si, offset message
mov dl, [si]
```

Here `SI` stores the address of `message`, and `[SI]` reads the byte at that address.

## Segment registers

| Register | Points to |
|---|---|
| `CS` | code segment |
| `DS` | data segment |
| `SS` | stack segment |
| `ES` | extra segment |

`CS` - code segment, stores the segment address of the memory area where program instructions are located.  
`DS` - data segment, stores the segment address of the memory area where variables and other data are located.  
`SS` - stack segment, stores the segment address of the memory area used as the stack.  
`ES` - extra segment, stores the segment address of an additional memory area for data.

Before accessing variables in `.data`, initialize `DS`:

```asm
mov ax, @data
mov ds, ax
```

## Instruction pointer and flags

| Register | Purpose |
|---|---|
| `IP` | offset of the next instruction |
| `FLAGS` | CPU status flags |

Common flags:
* `ZF` - zero flag
* `CF` - carry flag
* `SF` - sign flag
* `OF` - overflow flag

Flags are often changed by `cmp`, `add`, `sub` and used by jumps:

```asm
cmp ax, 0
je  is_zero
```

## int 21h usage

DOS interrupt functions usually use registers for input and output.

Example: output `$`-terminated string:

```asm
mov ah, 09h
mov dx, offset message
int 21h
```

Here:
* `AH` = function number
* `DX` = string offset
