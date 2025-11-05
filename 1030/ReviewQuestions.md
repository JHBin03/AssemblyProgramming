# Chapter 5.8 Review Questions and Exercises

## 5.8.1 Short Answer

**1.** Which instruction pushes all of the 32-bit general-purpose registers on the stack?
→ `PUSHAD`

**2.** Which instruction pushes the 32-bit EFLAGS register on the stack?
→ `PUSHFD`

**3.** Which instruction pops the stack into the EFLAGS register?
→ `POPFD`

**4.** Challenge: Another assembler (NASM) permits `PUSH EAX EBX ECX`.
Why might this be better than `PUSHAD`?
→ 모든 레지스터 대신 특정 레지스터만 선택적으로 푸시할 수 있으므로 스택 공간과 시간을 절약할 수 있음.

**5.** Challenge: Suppose there were no `PUSH` instruction.
Write a sequence that does the same as `push eax`.
→

```asm
sub esp, 4
mov [esp], eax
```

**6.** (True/False): The RET instruction pops the top of the stack into the instruction pointer.
→ **True**

**7.** (True/False): Nested procedure calls are not permitted unless the NESTED operator is used.
→ **False**

**8.** (True/False): In protected mode, each procedure call uses a minimum of 4 bytes of stack space.
→ **True**

**9.** (True/False): The ESI and EDI registers cannot be used when passing 32-bit parameters.
→ **False**

**10.** (True/False): The ArraySum procedure receives a pointer to any array of doublewords.
→ **True**

**11.** (True/False): The USES operator lets you name all registers modified within a procedure.
→ **True**

**12.** (True/False): The USES operator only generates PUSH instructions.
→ **False**
**13.** (True/False): The register list in USES must use commas to separate names.
→ **True**

**14.** Which statement(s) in ArraySum would change to handle 16-bit words?
→ `TYPE DWORD`를 `TYPE WORD`로 바꾸고, `EAX` 작업을 그에 맞게 조정.

**15.** What will be the final value in EAX after:

```asm
push 5
push 6
pop eax
pop eax
```

→ Final value: **5**

---

## 16. Code Analysis

```asm
main PROC
  push 10
  push 20
  call Ex2Sub
  pop eax
  INVOKE ExitProcess,0
main ENDP

Ex2Sub PROC
  pop eax
  ret
Ex2Sub ENDP
```

→ **Answer:** (b) Program halts with a runtime error on line 10
(Too many pops; stack imbalance.)

---

## 17. Code Analysis

```asm
main PROC
  mov eax,30
  push eax
  push 40
  call Ex3Sub
  INVOKE ExitProcess,0
main ENDP

Ex3Sub PROC
  pusha
  mov eax,80
  popa
  ret
Ex3Sub ENDP
```

→ **Answer:** (a) EAX will equal 40 on line 6
(`PUSHA`/`POPA` save and restore registers, so 80 is overwritten.)

---

## 18. Code Analysis

```asm
main PROC
  mov eax,40
  push offset Here
  jmp Ex4Sub
Here:
  mov eax,30
  INVOKE ExitProcess,0
main ENDP

Ex4Sub PROC
  ret
Ex4Sub ENDP
```

→ **Answer:** (a) EAX will equal 30 on line 7
(Return jumps to label Here.)

---

## 19. Code Analysis

```asm
main PROC
  mov edx,0
  mov eax,40
  push eax
  call Ex5Sub
  INVOKE ExitProcess,0
main ENDP

Ex5Sub PROC
  pop eax
  pop edx
  push eax
  ret
Ex5Sub ENDP
```

→ **Answer:** (b) The program will halt with a runtime error on line 13
(Stack imbalance—extra pop.)

---

## 20. Memory Exercise

```asm
.data
array DWORD 4 DUP(0)
.code
main PROC
  mov eax,10
  mov esi,0
  call proc_1
  add esi,4
  add eax,10
  mov array[esi],eax
  INVOKE ExitProcess,0
main ENDP
```

**Nested Calls:**

```asm
proc_1 PROC
  call proc_2
  add esi,4
  add eax,10
  mov array[esi],eax
  ret
proc_1 ENDP

proc_2 PROC
  call proc_3
  add esi,4
  add eax,10
  mov array[esi],eax
  ret
proc_2 ENDP

proc_3 PROC
  mov array[esi],eax
  ret
proc_3 ENDP
```

**결과:**

```
array = [10, 20, 30, 40]
```

---

## 5.8.2 Algorithm Workbench

**1.** Swap EAX and EBX using only PUSH/POP:

```asm
push eax
push ebx
pop eax
pop ebx
```

**2.** Move return address 3 bytes higher:

```asm
add dword ptr [esp], 3
```

**3.** Reserve local variables (two DWORDs) below return address:

```asm
sub esp, 8
mov [esp], 1000h
mov [esp+4], 2000h
```

**4.** Use indexed addressing to copy array elements in reverse:

```asm
mov esi, OFFSET array + SIZEOF array - 4
mov edi, OFFSET newArray
mov ecx, LENGTHOF array
L1: mov eax, [esi]
    mov [edi], eax
    sub esi, 4
    add edi, 4
    loop L1
```

**5.** Display subroutine’s return address safely:

```asm
mov eax, [esp]
call WriteHex
```
