# ReviewQuestions
## 1\. Provide examples of three different instruction mnemonics.

**MOV, ADD, JMP**

-----

## 2\. What is a calling convention, and how is it used in assembly language declarations?

\*\*Calling convention (호출 규약)\*\*은 함수(프로시저)가 호출될 때 **매개변수를 전달하는 방법**, **스택 정리 책임** (호출자/피호출자 중 누가 할지), **반환 값 위치**, **레지스터 사용 규칙** 등을 정의하는 표준화된 규칙이다.

어셈블리 언어 선언에서는 **`PROC`** 지시어를 사용하여 프로시저를 선언할 때 **`PROTO`** 지시어나 특정 어셈블러 문법(예: MASM의 **`proc`** 뒤에 \*\*`USES`\*\*와 함께)을 사용하여 이 호출 규약을 명시적으로 지정하거나 컴파일러가 암묵적으로 따르도록 한다.

-----

## 3\. How do you reserve space for the stack in a program?

**`.STACK`** 지시어를 사용하여 스택 세그먼트를 정의하고 필요한 크기(바이트)를 지정하여 공간을 예약한다.

-----

## 4\. Explain why the term assembler language is not quite correct.

정확한 명칭은 \*\*Assembly Language (어셈블리 언어)\*\*이며, \*\*Assembler (어셈블러)\*\*는 이 언어를 기계어로 번역하는 \*\*프로그램(번역기)\*\*을 의미하기 때문에 '어셈블러 언어'라는 표현은 정확하지 않다.

-----

## 5\. Explain the difference between big endian and little endian. Also, look up the origins of this term on the Web.

**Big Endian (빅 엔디안):** \*\*최상위 바이트(Most Significant Byte, MSB)\*\*를 메모리의 **가장 낮은 주소**에 저장하는 방식이다. (사람이 숫자를 읽는 방식과 유사하다.)

**Little Endian (리틀 엔디안):** \*\*최하위 바이트(Least Significant Byte, LSB)\*\*를 메모리의 **가장 낮은 주소**에 저장하는 방식이다. (x86 프로세서 계열에서 사용된다.)

**용어의 유래:** 이 용어는 1726년 \*\*조너선 스위프트(Jonathan Swift)\*\*가 쓴 풍자 소설 \*\*\<걸리버 여행기\>\*\*에서 유래했다. 소설 속 릴리푸트(Lilliput) 인들이 삶은 달걀을 깨 먹을 때 '큰 쪽 끝(Big End)'으로 깰지 '작은 쪽 끝(Little End)'으로 깰지를 두고 벌이는 사소한 전쟁을 풍자한 것에서 \*\*데니 코헨(Danny Cohen)\*\*이 1980년에 컴퓨터 과학에 이 용어를 도입했다.

-----

## 6\. Why might you use a symbolic constant rather than an integer literal in your code?

**가독성 향상:** 코드의 의미를 쉽게 이해할 수 있다 (예: `MAX_SIZE` 대신 `100`을 쓰는 대신).
**유지보수 용이:** 상수가 변경될 경우, 코드 전체에서 해당 값(숫자 리터럴)을 일일이 찾아서 수정할 필요 없이 **한 곳** (심볼릭 상수의 정의)만 수정하면 된다.

-----

## 7\. How is a source file different from a listing file?

**소스 파일 (Source File):** 프로그래머가 작성한 **어셈블리 언어 명령어와 지시어**가 담긴 파일이다 (예: `.asm`). 어셈블러의 **입력**이 된다.

**리스팅 파일 (Listing File):** 어셈블러가 소스 파일을 번역한 후 생성하는 파일로, **소스 코드 줄**과 그에 대응하는 **기계어 코드(16진수)**, **메모리 주소**, **데이터 오프셋** 등의 상세 정보를 포함한다. 디버깅 및 분석에 사용된다.

-----

## 8\. How are data labels and code labels different?

**데이터 레이블 (Data Label):** **변수**나 **상수**가 저장된 메모리의 \*\*주소(오프셋)\*\*를 나타낸다. (예: `.data` 세그먼트에서 사용)

**코드 레이블 (Code Label):** **실행 가능한 명령어**의 메모리 **주소**를 나타낸다. 프로그램 실행 흐름을 제어하는 \*\*`JMP`\*\*나 **`CALL`** 명령어의 **목표 지점**으로 사용된다.

-----

## 9\. (True/False): An identifier cannot begin with a numeric digit.

**True** (참)

-----

## 10\. (True/False): A hexadecimal literal may be written as 0x3A.

**False** (거짓) - 어셈블리 언어(MASM)에서 16진수 리터럴은 숫자로 시작하지 않을 경우 **h** 접미사를 사용하며, 숫자로 시작해야 할 경우 앞에 **0**을 붙여야 한다 (예: `3Ah` 또는 `03Ah`). `0x` 접두사는 C/C++에서 사용된다.

-----

## 11\. (True/False): Assembly language directives execute at runtime.

**False** (거짓) - 지시어는 **어셈블(번역) 시점**에 어셈블러에게 명령을 내릴 뿐, 프로그램 **실행(런타임) 시점**에는 아무런 코드도 생성하지 않는다.

-----

## 12\. (True/False): Assembly language directives can be written in any combination of uppercase and lowercase letters.

**True** (참) - 어셈블러는 일반적으로 지시어 및 명령어 **니모닉**의 대소문자를 구분하지 않는다.

-----

## 13\. Name the four basic parts of an assembly language instruction.

1.  **Label (레이블)**
2.  **Mnemonic (니모닉)**
3.  **Operand(s) (피연산자)**
4.  **Comment (주석)**

-----

## 14\. (True/False): MOV is an example of an instruction mnemonic.

**True** (참)

-----

## 15\. (True/False): A code label is followed by a colon (:), but a data label does not end with a colon.

**True** (참)

-----

## 16\. Show an example of a block comment.

```assembly
COMMENT ! 
    This is a block comment.
    It spans multiple lines.
    The assembler ignores everything until the next exclamation mark.
!
```

-----

## 17\. Why is it not a good idea to use numeric addresses when writing instructions that access variables?

변수에 접근할 때 숫자 주소를 사용하면 다음과 같은 문제가 발생한다:

1.  **가독성 저하:** 주소 자체는 변수의 목적을 설명해주지 못한다.
2.  **유지보수 어려움:** 프로그램에 새로운 변수를 추가하거나 기존 변수의 크기가 변경되면 모든 숫자 주소를 수동으로 변경해야 한다. \*\*레이블(심볼릭 이름)\*\*을 사용해야 어셈블러가 주소 계산을 자동으로 처리해준다.

-----

## 18\. What type of argument must be passed to the ExitProcess procedure?

프로그램의 \*\*종료 상태 코드(Exit Code)\*\*를 나타내는 **32비트 정수** (DWORD) 인수가 전달되어야 한다. (일반적으로 성공 시 0을 전달한다.)

-----

## 19\. Which directive ends a procedure?

**ENDP** (End Procedure) 지시어

-----

## 20\. In 32-bit mode, what is the purpose of the identifier in the END directive?

**`END`** 지시어에 지정된 식별자(identifier)는 프로그램의 **시작점(entry point)**, 즉 실행이 시작되어야 할 **첫 번째 코드 레이블**을 어셈블러에게 알려주는 역할을 한다.

-----

## 21\. What is the purpose of the PROTO directive?

**PROTO** (Prototype) 지시어는 다른 어셈블리 모듈이나 라이브러리에 정의된 프로시저(함수)의 **이름**, **매개변수 목록**, **데이터 형식** 등을 선언하여, 호출자가 해당 프로시저를 올바른 형식으로 호출할 수 있도록 **컴파일러(어셈블러)에게 알려주는 역할**을 한다.

-----

## 22\. (True/False): An Object file is produced by the Linker.

**False** (거짓) - 오브젝트 파일(Object file, `.obj`)은 \*\*어셈블러(Assembler)\*\*에 의해 생성된다. 링커(Linker)는 오브젝트 파일을 입력받아 실행 파일(`.exe`)을 생성한다.

-----

## 23\. (True/False): A Listing file is produced by the Assembler.

**True** (참)

-----

## 24\. (True/False): A link library is added to a program just before producing an Executable file.

**True** (참) - 링커(Linker)가 오브젝트 파일과 **링크 라이브러리**를 결합하여 최종 실행 파일(Executable file)을 생성한다.

-----

## 25\. Which data directive creates a 32-bit signed integer variable?

**SDWORD** (Signed Double Word)

-----

## 26\. Which data directive creates a 16-bit signed integer variable?

**SWORD** (Signed Word)

-----

## 27\. Which data directive creates a 64-bit unsigned integer variable?

**QWORD** (Quad Word)

-----

## 28\. Which data directive creates an 8-bit signed integer variable?

**SBYTE** (Signed Byte)

-----

## 29\. Which data directive creates a 10-byte packed BCD variable?

**TBYTE** (Ten Byte)

# Algorithm Workbench

## 1\. Define four symbolic constants that represent integer 25 in decimal, binary, octal, and hexadecimal formats.

```assembly
.CONST
DEC_25 = 25d
BIN_25 = 11001b
OCT_25 = 31o
HEX_25 = 19h
```

-----

## 2\. Find out, by trial and error, if a program can have multiple code and data segments.

**Yes** (가능하다)

-----

## 3\. Create a data definition for a doubleword that stored it in memory in big endian format.

```assembly
.DATA
bigEndianVal DWORD BIG ENDIAN 87654321h
```

-----

## 4\. Find out if you can declare a variable of type DWORD and assign it a negative value. What does this tell you about the assembler’s type checking?

**Yes** (가능하다). 어셈블러는 **`DWORD`** 변수에 `-1`과 같은 음수 값을 할당하는 것을 허용하며, 이는 일반적으로 해당 음수 값의 **2의 보수(Two's Complement)** 표현을 변수에 저장하게 된다. 이는 어셈블러가 \*\*타입 체크(Type Checking)\*\*를 엄격하게 하지 않고, 정의된 크기(DWORD는 32비트) 내에서 **부호 있는(signed) 값**이나 **부호 없는(unsigned) 값**을 모두 유연하게 처리함을 보여준다.

-----

## 5\. Write a program that contains two instructions: (1) add the number 5 to the EAX register, and (2) add 5 to the EDX register. Generate a listing file and examine the machine code generated by the assembler. What differences, if any, did you find between the two instructions?

차이점: **Opcode와 ModR/M 바이트가 다르다.**

  - `ADD EAX, 5`: `EAX` 레지스터는 일반적으로 특수한 단축 형식 Opcode를 사용하여 더 간결한 기계어 코드(예: `83 C0 05` 또는 `05 05 00 00 00` 등)를 가질 수 있다.
  - `ADD EDX, 5`: `EDX` 레지스터는 일반적인 `Opcode + ModR/M + SIB + Displacemnet` 형식을 따라 `EAX`와는 다른 바이트(특히 레지스터를 지정하는 **ModR/M 바이트**)를 사용한다.

-----

## 6\. Given the number 456789ABh, list out its byte values in little-endian order.

**ABh, 89h, 67h, 45h** (가장 낮은 바이트인 `ABh`가 가장 낮은 주소에 위치한다.)

-----

## 7\. Declare an array of 120 uninitialized unsigned doubleword values.

```assembly
.DATA?
dWordArray DWORD 120 DUP(?)
```

-----

## 8\. Declare an array of byte and initialize it to the first 5 letters of the alphabet.

```assembly
.DATA
bArray BYTE 'A', 'B', 'C', 'D', 'E'
```

-----

## 9\. Declare a 32-bit signed integer variable and initialize it with the smallest possible negative decimal value. (Hint: Refer to integer ranges in Chapter 1.)

```assembly
.DATA
sInt32 SDWORD -2147483648
```

-----

## 10\. Declare an unsigned 16-bit integer variable named wArray that uses three initializers.

```assembly
.DATA
wArray WORD 10, 20, 30
```

-----

## 11\. Declare a string variable containing the name of your favorite color. Initialize it as a null-terminated string.

```assembly
.DATA
myColor BYTE "Blue", 0
```

-----

## 12\. Declare an uninitialized array of 50 signed doublewords named dArray.

```assembly
.DATA?
dArray SDWORD 50 DUP(?)
```

-----

## 13\. Declare a string variable containing the word “TEST” repeated 500 times.

```assembly
.DATA
testString BYTE 500 DUP("TEST")
```

-----

## 14\. Declare an array of 20 unsigned bytes named bArray and initialize all elements to zero.

```assembly
.DATA
bArray BYTE 20 DUP(0)
```

-----

## 15\. Show the order of individual bytes in memory (lowest to highest) for the following doubleword variable:

**val1 DWORD 87654321h**

| 메모리 주소 | 저장된 바이트 |
| :---: | :---: |
| val1 (가장 낮은 주소) | **21h** |
| val1 + 1 | **43h** |
| val1 + 2 | **65h** |
| val1 + 3 (가장 높은 주소) | **87h** |
