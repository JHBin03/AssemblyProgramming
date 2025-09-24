
# Review Questions

## | 1 | In 32-bit mode, aside from the stack pointer (ESP), what other register points to variables on the stack? |
EBP (Extended Base Pointer) |
## | 2 | Name at least four CPU status flags. |
CF, ZF, SF, OF (Carry, Zero, Sign, Overflow Flag) |
## | 3 | Which flag is set when the result of an **unsigned** arithmetic operation is too large to fit into the destination? |
CF (Carry Flag) |
## | 4 | Which flag is set when the result of a **signed** arithmetic operation is either too large or too small to fit into the destination?
| OF (Overflow Flag) |
## | 5 | (True/False): When a register operand size is 32 bits and the REX prefix is used, the R8D register is available for programs to use.
| False |
## | 6 | Which flag is set when an arithmetic or logical operation generates a negative result?
| SF (Sign Flag) |
## | 7 | Which part of the CPU performs floating-point arithmetic?
| FPU (Floating-Point Unit) 또는 SSE/Execution Units |
## | 8 | On a 32-bit processor, how many bits are contained in each floating-point data register?
| 80 bits |
## | 9 | (True/False): The x86-64 instruction set is backward-compatible with the x86 instruction set.
| True |
## | 10 | (True/False): In current 64-bit chip implementations, all 64 bits are used for addressing.
| False |
## | 11 | (True/False): The Itanium instruction set is completely different from the x86 instruction set.
| True |
## | 12 | (True/False): Static RAM is usually less expensive than dynamic RAM.
| False |
## | 13 | (True/False): The 64-bit RDI register is available when the REX prefix is used.
| True |
## | 14 | (True/False): In native 64-bit mode, you can use 16-bit real mode, but not the virtual-8086 mode.
| False |
## | 15 | (True/False): The x86-64 processors have 4 more general-purpose registers than the x86 processors.
| False |
## | 16 | (True/False): The 64-bit version of Microsoft Windows does not support virtual-8086 mode.
| True |
## | 17 | (True/False): DRAM can only be erased using ultraviolet light.
| False |
## | 18 | (True/False): In 64-bit mode, you can use up to eight floating-point registers. 
| False |
## | 19 | (True/False): A bus is a plastic cable that is attached to the motherboard at both ends, but does not sit directly on the motherboard.
| False |
## | 20 | (True/False): CMOS RAM is the same as static RAM, meaning that it holds its value without any extra power or refresh cycles.
| False |
##  | 21 | (True/False): PCI connectors are used for graphics cards and sound cards.
| True |
## | 22 | (True/False): The 8259A is a controller that handles external interrupts from hardware devices.
| True |
## | 23 | (True/False): The acronym PCI stands for programmable component interface.
| False |
## | 24 | (True/False): VRAM stands for virtual random access memory.
| False |
## | 25 | At what level(s) can an assembly language program manipulate input/output?
| 하드웨어 수준 / 운영체제 시스템 호출 수준 |
## | 26 | Why do game programs often send their sound output directly to the sound card's hardware ports?
| 지연 시간 최소화 및 CPU 오버헤드 감소 (실시간 성능을 위함) |
