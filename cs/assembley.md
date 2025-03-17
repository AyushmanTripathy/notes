# Learning Assembley

from :- [DaedalusCommunity](https://www.youtube.com/watch?v=MwPjvJ9ulSc&t=204s)

## Variables

- 16 bit address, now
- bx now points to string hello

```asm
org 0x7c00
mov bx, name
name:
    db "Hello", 0
```

## Stack

- base pointer (bp) and stack/top pointer (sp)
- __NOTE__: sp moves back

```
mov bp, 0x8000
mov sp, bp
push ax
pop ax
```

- push and pop all registers
- ax, cx, dx, bx, sp, bp, si, di push in this order

```
pusha
popa
```

## Procedure

- how a procedure is implemented

```
    pusha
    jmp print
return:
    popa

    jmp end ; avoid infinte loop


print:
  mov ah, 0x0e
  mov al, 'E'
  int 0x10
  jmp return
```

- call adds syntactic sugar
- pusha and popa is still done manually

```
    call print
    jmp end

print:
    pusha
    mov ah, 0x0e
    mov al, 'E'
    int 0x10
    popa
    ret
```

- `eax` is used for returns
- `edi` and `esi` are argument 1 and argument 2

## Segmentation

- divides memory into, 64KiB chunks
- hence addressable by 16 bit address
- data (ds), code (cs), stack (ss) and extra (es) segments

```
address = ds * 16 + offset
address = ds : offset
```

- tiny model, ds = ss = cs = 0
