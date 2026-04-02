# Output strings and chars

[← back](../index.md)

## Output a string, terminated by $

```asm
mov		ah, 09h
mov		dx, offset message
int		21h
```

The string should be defined after the `end program` statement:
```asm
message		db	"Green dragons fly at night$"
```
Also you can use CR/LF symbols to define multi-line strings:
```asm
message		db	"Are you gangsters?",0Dh,0Ah,"Yes, we are!$"
```

## Output a single char

```asm
mov		ah, 02h
mov		dl, "X"
int		21h
```

## Output a string char-by-char

Output of the null-terminated string:
```asm
		mov		si, offset message
next:
		cmp		byte ptr [si], 0	; byte ptr == take 1 byte by this address
		je		finish

		mov		ah, 02h
		mov		dl, [si]			; DL is 1 byte, so no need to use "byte ptr"
		int		21h

		inc		si
		jmp		next
finish:		
```

The `message` is defined as a null-terminated string:
```asm
message		db	"Green dragons fly at night", 0
```