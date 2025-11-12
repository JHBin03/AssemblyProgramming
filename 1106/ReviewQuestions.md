1. What will be the value of BX after the following instructions execute?
   mov bx,0FFFFh
   and bx,68h
   **답:** BX = 0068h

---

2. What will be the value of BX after the following instructions execute?
   mov bx,912Ah
   and bx,92h
   **답:** BX = 0082h

---

3. What will be the value of BX after the following instructions execute?
   mov bx,0649Bh
   or bx,3Ah
   **답:** BX = 64BBh

---

4. What will be the value of BX after the following instructions execute?
   mov bx,029D6h
   xor bx,8181h
   **답:** BX = 8B57h

---

5. What will be the value of EBX after the following instructions execute?
   mov ebx,0AFAF649Bh
   or ebx,3A219604h
   **답:** EBX = BFAFF69Fh

---

6. What will be the value of RBX after the following instructions execute?
   mov rbx,0AFAF649Bh
   xor rbx,0FFFFFFFFh
   **답:** RBX = F0509B64h

---

7. In the following instruction sequence, show the resulting value of AL where indicated, in binary:
   (a) mov al,01101111b / and al,00101101b → **00101101b**
   (b) mov al,6Dh / and al,4Ah → **01001000b**
   (c) mov al,00001111b / or al,61h → **01101111b**
   (d) mov al,94h / xor al,37h → **10110111b**

---

8. In the following instruction sequence, show the resulting value of AL where indicated, in hexadecimal:
   (a) mov al,7Ah / not al → **85h**
   (b) mov al,3Dh / and al,74h → **34h**
   (c) mov al,98h / or al,35h → **BDh**
   (d) mov al,72h / xor al,0DCh → **AEh**

---

9. In the following instruction sequence, show the values of the Carry, Zero, and Sign flags where indicated:
   (a) mov al,00001111b / test al,00000101b → CF=0 ZF=0 SF=0
   (b) mov al,00000101b / cmp al,00001011b → CF=1 ZF=0 SF=1
   (c) mov al,00000101b / cmp al,00000111b → CF=1 ZF=0 SF=0

---

10. Which conditional jump instruction executes a branch based on the contents of ECX?
    **답:** LOOP, LOOPZ, LOOPNZ

---

11. How are JA and JNBE affected by the Zero and Carry flags?
    **답:** ZF=0, CF=0일 때 점프함 (둘 다 0이면 참)

---

12. What will be the final value in EDX after this code executes?
    mov edx,1
    mov eax,7FFFh
    cmp eax,8000h
    jl L1
    mov edx,0
    L1:
    **답:** EDX = 1

---

13. What will be the final value in EDX after this code executes?
    mov edx,1
    mov eax,7FFFh
    cmp eax,8000h
    jb L1
    mov edx,0
    L1:
    **답:** EDX = 1

---

14. What will be the final value in EDX after this code executes?
    mov edx,1
    mov eax,7FFFh
    cmp eax,0FFFF8000h
    jl L2
    mov edx,0
    L2:
    **답:** EDX = 0

---

15. (True/False): The following code will jump to the label named Target.
    mov eax,-30
    cmp eax,-50
    jg Target
    **답:** True

---

16. (True/False): The following code will jump to the label named Target.
    mov eax,-42
    cmp eax,26
    ja Target
    **답:** False

---

17. What will be the value of RBX after the following instructions execute?
    mov rbx,0FFFFFFFFFFFFFFFFh
    and rbx,80h
    **답:** RBX = 80h

---

18. What will be the value of RBX after the following instructions execute?
    mov rbx,0FFFFFFFFFFFFFFFFh
    and rbx,808080h
    **답:** RBX = 808080h

---

19. What will be the value of RBX after the following instructions execute?
    mov rbx,0FFFFFFFFFFFFFFFFh
    and rbx,80808080h
    **답:** RBX = 80808080h

---
### 6.10.2 Algorithm Workbench

1. **ASCII 숫자 변환**
   `AL`에 ASCII 숫자(‘0’~‘9’)가 있을 경우 이를 이진 값(00h~09h)으로 변환.

```asm
sub al, 30h
```

---

2. **32비트 피연산자의 패리티 계산**
   32비트 메모리 피연산자의 패리티를 계산하여 결과를 0 또는 1로 반환.

```asm
xor al, [operand]       ; 처음 바이트
xor al, [operand+1]
xor al, [operand+2]
xor al, [operand+3]
```

→ `AL`의 parity flag를 통해 짝/홀 판단 가능.

---

3. **두 비트맵 SetX, SetY 비교**
   SetX에는 속하지만 SetY에는 없는 멤버를 나타내는 비트열 생성.

```asm
mov eax, SetX
not ebx          ; SetY 반전
and eax, ebx     ; X ∧ ¬Y
```

---

4. **DX ≤ CX일 때 L1으로 점프 (Unsigned)**

```asm
cmp dx, cx
jbe L1
```

---

5. **AX > CX일 때 L2로 점프 (Signed)**

```asm
cmp ax, cx
jg L2
```

---

6. **AL의 0비트와 1비트를 검사 후 점프**
   결과가 0이면 L3으로, 아니면 L4로 점프.

```asm
test al, 00000011b
jz L3
jmp L4
```

---

7. **단축 평가 논리 (1)**

```asm
cmp val1, ecx
ja skip1
cmp ecx, edx
ja skip1
mov x, 1
jmp done
skip1:
mov x, 2
done:
```

`if (val1 > ecx) AND (ecx > edx)` 형태 구현.

---

8. **단축 평가 논리 (2)**

```asm
cmp ebx, ecx
jg set1
cmp ebx, val1
jg set1
mov x, 2
jmp done
set1:
mov x, 1
done:
```

`if (ebx > ecx) OR (ebx > val1)` 형태 구현.

---

9. **복합 조건 단축 평가 (3)**

```asm
cmp ebx, ecx
jle next
cmp ebx, edx
jle next
cmp edx, eax
jle next
mov x, 1
jmp done
next:
mov x, 2
done:
```

`if (ebx > ecx AND ebx > edx) OR (edx > eax)` 표현.

---

10. **While 반복문 변환**

```asm
while_loop:
cmp N, 0
jle end_loop
cmp N, 3
je not_equal3
cmp N, A
jl skip_sub
cmp N, B
jg skip_sub
not_equal3:
sub N, 2
jmp while_loop
skip_sub:
dec N
jmp while_loop
end_loop:
```

`while N > 0` 내부에 조건문 포함한 복합 루프 구조 구현.
