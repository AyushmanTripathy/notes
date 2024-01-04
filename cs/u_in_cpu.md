# Putting the U in CPU

from: [cpu.land](https://cpu.land/)

### The Basics

- machine code is binary instructions in a row
- opcode (the instruction) followed by required data
- assembly is human friendly syntax for machine code

```
add     ebx,    10      (assembly)
0x83    0xC3    0x0A    (machine code)
```

- Little Endian, last byte of multi-byte data type is stored first
- Big Endian, first byte is stored first

### RAM

- stores all data including program code
- program code is stored as machine code
- instruction pointer `IP` register -> address of the next instruction
- process are OS level abstractions

### Kernel

- after booting, IP starts at kernel
- linux, Windows NT, XNU for macOS

### Rings

- mode / privilege level / ring decides what processor is allowed to do
- on x86-64, CPL (current privilege level) is 2 least sig digit of `cp` register
- 00 ring -> kernel, 11 ring -> user
- 01 and 10 used for drivers

### System Call

- let program code jump to kernel code
- done using software interrupts
- during boot, interrupt vector tabel (IVT) maps interrupts no to code pointer
- userland progs used instruction (like INT) to use a software interrupt
- kernel code uses IRET to switch to user mode and change IP

### Interrupt

- processor suspends current activity, saves state and executes interrupt
  handler
- used to implement system calls, multitasking etc
- for example, `INT 0x80` for system calls
- can be software (triggered by a program) or hardware (by timer chips)

### Wrapper APIs

- resuable higher level library functions
- `libc` for Unix, `ntdll.dll` for Windows
- they do platform dependent system call for you 

### CISC

- complex instruction set computer
- example `x86-64`
- single instruction does several operations
- needed because RAM is compared to CPU

- `SYSCALL` and `SYSENTER` are optimised alternatives to `INT 0x80`
- `SYSRET` and `SYSEXIT` for `IRET`

### RISC

- opposite to CISC
- example `AArch64` used in Apple Silicon
- has only INT and IRET

### Preemptive Multitasking

- fake parallelism by letting process take turns on CPU
- example of timer chips, PITs (Programmable interval timers)
- before jumping to program code, timer chip is set
- when time elapses, hardware interrupt is triggered
- jumps to OS code, OS saves where program left off, load diff program, repeat

- Preemption, interruption of a process
- kernel code is also preemptive
- opposite: Cooperative Multitasking, progs give control on their own

### Timeslice Calculation

- timeslice is duration a process can run before preempting.
- called `quantums`
- diff scheduling algos are

1. fixed timeslice round-robin
2. naive dynamic timeslice round-robin

- target latency, time to resume process execution after preempting.
- it is a ideal time, decided by os devs
- timeslice = target latency / no of process
- minimum granularity can exceed target latency
- since process switching is heavy.


### Exec Syscalls

- shebangs are used by kernel and turnicated by 256 bytes
- first iterates through binfmt (binary format) handlers to find a match
- handler than perform execution.

- for ELF format,
- `PT_LOAD` is loaded into memory
- `PT_INTERP` is loaded into memory if present (which is ld)
- if dynamic linking, CPU starts at `PT_INTERP` else at executable


### ELF format

- Executable and Linkable format
- like PE (Portable Executable in .exe files) or Mach-O (on MacOS) 
- handled by `binfmt_elf`
- file structure, 

1. ELF Header

- what processor, entry point, if it a dll

1. Program Header Table

- `PT_LOAD`, `PT_INTERP`, `PT_DYNAMIC` etc
- what virtual memory address data to be loaded in
- length of data and length of memory region
- BSS is empty region, maybe used at runtime (filled with 0s)
- permission flags (RWX)

1. Section Header Table

- map for data in ELF
- not required for execution, used by Debuggers.

1. Actual Data

### Linking

- static linking means copying code at build time from developer's computer
- dynamic linking code loaded from user computer at runtime
- Linux .so (Shared Object), windows .dll (dynamic link library), MacOS .dylib
- static linking loads only required portions
- dynamic linking loads whole library, saves memory as it is shared

- linker (ld) replaces named pointers to jump instructions
