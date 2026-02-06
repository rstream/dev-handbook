# Hello world application in Assembler

[← back](index.md)

This is a sample "Hello World" application written in Assembler for MS-DOS

```asm
.model tiny                 ; single segment for code and data
.code                       ; code segment begin

org 100h                    ; code begins from here (offset from the beginning of app's segment)

start:                      ; begin

        mov dx, offset msg  ; get offset of msg
        mov ah, 9h          ; 9h = write to screen (until first "$")
        int 21h             ; do it!

        mov ax, 4c00h       ; finish program
        int 21h             ; do it!

msg db 'Hello World!$'      ; define bytes (db): var msg = "Hello$";
end start                   ; end (everything after this line is ignored)
```