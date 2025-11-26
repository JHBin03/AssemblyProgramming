# 8 Review Questions

1. Which statements belong in a procedure’s epilogue when the procedure has stack parameters and local variables?
답: 저장된 레지스터 복원(pop), 지역 변수 해제(mov esp, ebp), 베이스 포인터 복원(pop ebp), ret 명령이 포함된다.

---
2. When a C function returns a 32-bit integer, where is the return value stored?
답: EAX 레지스터에 저장된다.

---
3. How does a program using the STDCALL calling convention clean up the stack after a procedure call?
답: 피호출자(callee)가 ret n 형식으로 스택을 정리한다.

---
4. How is the LEA instruction more powerful than the OFFSET operator?
답: OFFSET은 변수의 정적 주소만 가져오지만, LEA는 실행 중 계산된 유효 주소를 계산할 수 있어 더 유연하다.

---
5. In the C++ example shown in Section 8.2.3, how much stack space is used by a variable of type int?
답: 4바이트가 사용된다.

---
6. What advantages might the C calling convention have over the STDCALL calling convention?
답: CDECL은 호출자가 스택을 정리하기 때문에 가변 인자 함수(printf 등) 구현에 유리하다.

---
7. (True/False): When using the PROC directive, all parameters must be listed on the same line.
답: False. 여러 줄에 나누어 작성할 수 있다.

---
8. (True/False): If you pass a variable containing the offset of an array of bytes to a procedure that expects a pointer to an array of words, the assembler will flag this as an error.
답: True. 자료형이 일치하지 않아 오류가 발생한다.

---
9. (True/False): If you pass an immediate value to a procedure that expects a reference parameter, you can generate a general-protection fault.
답: True. 참조 매개변수는 주소를 요구하는데 즉시값을 넘기면 잘못된 메모리 접근이 발생한다.

# Algorithm Workbench

1. Here is a calling sequence for a procedure named AddThree that adds three doublewords  
(assume that the STDCALL calling convention is used):

    push 10h  
    push 20h  
    push 30h  
    call AddThree  

   Draw a picture of the procedure’s stack frame immediately after EBP has been pushed on the runtime stack.
답:  
EBP가 push된 직후의 스택 프레임은 다음과 같다(위 → 아래):

[EBP+12] = 첫 번째 인자 10h  
[EBP+8]  = 두 번째 인자 20h  
[EBP+4]  = 세 번째 인자 30h  
[EBP]    = 이전 EBP  
[EBP-4] 이후 = 지역 변수 공간(존재한다면)

---

2. Create a procedure named AddThree that receives three integer parameters and calculates and returns their sum in the EAX register.
답:  
세 개의 파라미터는 [ebp+8], [ebp+12], [ebp+16]에 위치하며,  
EAX에 더한 값을 넣어 반환한다.

---

3. Declare a local variable named pArray that is a pointer to an array of doublewords.
답:  
`LOCAL pArray:PTR DWORD`  
형식으로 선언한다.

---

4. Declare a local variable named buffer that is an array of 20 bytes.
답:  
`LOCAL buffer[20]:BYTE`  
형식으로 선언한다.

5. Declare a local variable named pwArray that points to a 16-bit unsigned integer.
답:  
LOCAL pwArray:PTR WORD  
형식으로 선언한다.

---
6. Declare a local variable named myByte that holds an 8-bit signed integer.
답:  
LOCAL myByte:SBYTE  
형식으로 선언한다.

---
7. Declare a local variable named myArray that is an array of 20 doublewords.
답:  
LOCAL myArray[20]:DWORD  
형식으로 선언한다.

---
8. Create a procedure named SetColor that receives two stack parameters: forecolor and backcolor, and calls the SetTextColor procedure from the Irvine32 library.
답:  
두 개의 파라미터는 각각 [ebp+8], [ebp+12] 위치에 있으며,  
이를 SetTextColor(전경색, 배경색) 형태로 호출하는 PROC을 작성하면 된다.

---
9. Create a procedure named WriteColorChar that receives three stack parameters: char, forecolor, and backcolor. It displays a single character, using the color attributes specified in forecolor and backcolor.
답:  
스택 파라미터는 [ebp+8] = char, [ebp+12] = forecolor, [ebp+16] = backcolor  
세 값을 받아 문자 출력 전 색상 설정 후 문자 출력, 그리고 원래 색 복원 과정을 포함해야 한다.

---
10. Write a procedure named DumpMemory that encapsulates the DumpMem procedure in the Irvine32 library. Use declared parameters and the USES directive.  
The following is an example of how it should be called:  
INVOKE DumpMemory, OFFSET array, LENGTHOF array, TYPE array
답:  
DumpMemory는 OFFSET(배열 주소), LENGTHOF(길이), TYPE(자료형 크기)을  
스택으로 받아 Irvine32의 DumpMem을 내부에서 호출하는 래퍼(wrapper) PROC을 작성하면 된다.

---
11. Declare a procedure named MultArray that receives two pointers to arrays of doublewords, and a third parameter indicating the number of array elements. Also, create a PROTO declaration for this procedure.
답:  
PROTO는  
MultArray PROTO, pA:PTR DWORD, pB:PTR DWORD, count:DWORD  
형식으로 선언하고, PROC에서도 동일한 파라미터 리스트를 사용하면 된다.
