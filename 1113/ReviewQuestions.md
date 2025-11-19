# Short Answer Solutions

(1) In the following code sequence, show the value of AL after each shift or rotate instruction has executed:
답:
a. 6Ah  
b. EAh  
c. FDh  
d. A9h  
------------
(2) In the following code sequence, show the value of AL after each shift or rotate instruction has executed:
답:
a. 9Ah  
b. 6Ah  
c. A9h  
d. 3Ah  
------------
(3) What will be the contents of AX and DX after the following operation?

mov dx,0  
mov ax,222h  
mov cx,100h  
mul cx  

답: AX=2200h, DX=0002h  
------------
(4) What will be the contents of AX after the following operation?

mov ax,63h  
mov bl,10h  
div bl  

답: AX=0306h  
------------
(5) What will be the contents of EAX and EDX after the following operation?

mov eax,123400h  
mov edx,0  
mov ebx,10h  
div ebx  

답: EAX=00012340h, EDX=00000000h  
------------
(6) What will be the contents of AX and DX after the following operation?

mov ax,4000h  
mov dx,500h  
mov bx,10h  
div bx  

답: Divide Overflow (결과 정의되지 않음)  
------------
(7) What will be the contents of BX after the following instructions execute?

mov bx,5  
stc  
mov ax,60h  
adc bx,ax  

답: BX=0066h  
------------
(8) Describe the output when the following code executes in 64-bit mode:

mov rdx,dividend_hi  
mov rax,dividend_lo  
div divisor  

답:  
RAX = 1080000003330000h  
RDX = 20h  
------------
(9) The following program is supposed to subtract val2 from val1. Find and correct all logic errors.

답:  
mov cx,8  
mov rsi,val1  
mov rdi,val2  
mov rbx,result  
clc  
top:  
    mov al,[rsi]  
    sbb al,[rdi]  
    mov [rbx],al  
    inc rsi  
    inc rdi  
    inc rbx  
loop top  
------------
(10) What will be the hexadecimal contents of RAX after the following instructions execute in 64-bit mode?

imul rax,multiplicand,4  

답: RAX = 0004080C10140000h  
------------



# Algorithm Workbench

1. Write a sequence of shift instructions that cause AX to be sign-extended into EAX.
답:
SAR AX,15 / SHL EAX,16 / SAR EAX,16
----
2. Suppose the instruction set contained no rotate instructions. Show how you would use SHR and a conditional jump instruction to rotate the contents of AL right 1 bit.
답:
SHR AL,1 후 CF 확인하여 MSB를 조건 분기(JC/JNC)로 설정
----
3. Write a logical shift instruction that multiplies the contents of EAX by 16.
답:
SHL EAX,4
----
4. Write a logical shift instruction that divides EBX by 4.
답:
SHR EBX,2
----
5. Write a single rotate instruction that exchanges the high and low halves of the DL register.
답:
ROL DL,4
----
6. Write a single SHLD instruction that shifts the highest bit of AX into the lowest bit of DX and shifts DX one bit to the left.
답:
SHLD DX,AX,1
----
7. Write a sequence of instructions that shift three memory bytes to the right by 1 bit position.
답:
mov al,byteArray+2 / shr al,1 / mov byteArray+2,al  
mov al,byteArray+1 / rcr al,1 / mov byteArray+1,al  
mov al,byteArray / rcr al,1 / mov byteArray,al
----
8. Write a sequence of instructions that shift three memory words to the left by 1 bit position.
답:
mov ax,wordArray / shl ax,1 / mov wordArray,ax  
mov ax,wordArray+2 / rcl ax,1 / mov wordArray+2,ax  
mov ax,wordArray+4 / rcl ax,1 / mov wordArray+4,ax
----
9. Write instructions that multiply –5 by 3 and store the result in a 16-bit variable.
답:
mov ax,-5 / imul ax,3 / mov result,ax (결과 = -15)
----
10. Write instructions that divide –276 by 10 and store the result in a 16-bit variable val1.
답:
mov ax,-276 / cwd / mov bx,10 / idiv bx / mov val1,ax (몫=-27, 나머지=-6)
----
11. Implement the following C++ expression (unsigned 32-bit):
val1 = (val2 * val3) / (val4 - 3)
답:
mov eax,val2 / mul val3 / mov ebx,val4 / sub ebx,3 / div ebx / mov val1,eax
----
12. Implement the following C++ expression (signed 32-bit):
val1 = (val2 / val3) * (val1 + val2)
답:
mov eax,val2 / cdq / idiv val3 / mov ebx,eax  
mov eax,val1 / add eax,val2 / imul eax,ebx / mov val1,eax
----
13. Write a procedure that displays an unsigned 8-bit binary value in decimal format (0~99).
답:
10으로 나누어 quotient=10의 자리, remainder=1의 자리  
각각 '0' 더해 WriteChar로 출력
----
14. Challenge: AAA with AX=0072h, AF=1.
답:
AL=02h, AH=00h, CF=1 (AAA 결과)
----
15. Challenge: compute x mod y using only SUB, MOV, AND, NOT (y=2^n).
답:
x AND (y-1)
----
16. Challenge: sign-extend the signed integer in AX into EAX using only SAR, ADD, XOR.
답:
SAR AX,15 로 AX 부호 확장  
XOR/ADD 조합으로 EAX 상위 비트에 동일 부호 반영  
(SAR 기반 부호비트 복제)
----

