Chapter 5. Procedures

### 1. Stack 기본 개념

* **LIFO (Last In First Out)** 구조.
  → 나중에 넣은 데이터가 먼저 나온다.
* **Stack Pointer (ESP)**: 스택의 최상단 데이터를 가리키는 CPU 레지스터.
* **메모리 구조**

  * 스택은 평소와 **반대로 그림**:
    상단이 낮은 주소, 하단이 높은 주소.

---

### 2. Stack Operation

#### PUSH

* 동작:

  1. ESP를 데이터 크기만큼 **감소**시킨다.
  2. 해당 위치에 데이터를 저장.
* 즉, 스택이 **아래로 확장**되는 구조.
* 관련 명령:

  * `PUSH <data>`
  * `PUSHFD` → EFLAGS 전체를 스택에 저장.
  * `PUSHAD` →
    EAX → ECX → EDX → EBX → (ESP before) → EBP → ESI → EDI 순으로 저장.

#### POP

* 동작:

  1. ESP가 가리키는 값을 꺼내 목적지 레지스터로 이동.
  2. ESP를 **데이터 크기만큼 증가**시킴.
* 예시:

  ```asm
  POP EAX
  ```

---

### 3. Stack의 활용

| 용도       | 설명                    |
| -------- | --------------------- |
| 지역 변수 저장 | 함수 내에서 임시 저장 공간으로 사용  |
| 인자 전달    | 함수 호출 시 파라미터 전달       |
| 레지스터 백업  | PUSH/POP으로 일시 저장 후 복구 |
| 리턴 주소 저장 | CALL 명령 시 자동으로 push됨  |

---

### 4. 예시 – PUSHAD / POPAD

```asm
MySub PROC
  PUSHAD
  ; ... do something ...
  POPAD
  RET
MySub ENDP
```

* 작업 전 레지스터 상태를 모두 저장하고, 복귀 시 복구함.
* “다른 곳으로 갔다가 돌아와야 하는 작업”에서 유용.

---

### 5. 문자열을 스택에 저장하고 꺼내기

```asm
.data
aName BYTE "I like StarII",0
nameSize = ($ - aName) - 1 ; 12

.code
mov ecx, nameSize
mov esi, 0
L1: movzx eax, aName[esi]
    push eax
    inc esi
loop L1

mov ecx, nameSize
mov esi, 0
L2: pop eax
    mov aName[esi], al
    inc esi
loop L2
```

* 문자를 순서대로 push했다가 pop하면 **역순으로 재배열**된다.
  (스택의 LIFO 구조 확인 예시)

---

### 6. Procedure (Subroutine)

#### 정의

* 특정 작업을 수행하는 코드 블록.
  → 다른 언어의 함수(Function)와 유사.
* `PROC`와 `ENDP` 사이에 정의.
* **RET**: 호출한 위치로 복귀.

#### 예시

```asm
SumOf PROC
  add eax, ebx
  add eax, ecx
  ret
SumOf ENDP
```

#### CALL & RET 작동 방식

* `CALL` → 다음 명령의 주소(IP)를 **스택에 push**.
* `RET` → 스택에서 주소를 **pop**하여 복귀.

---

### 7. Argument 전달 방식

* 일반적으로 **레지스터로 전달**:

  ```asm
  mov eax, 10000h
  mov ebx, 20000h
  mov ecx, 30000h
  call SumOf
  ```
* 리턴값은 **EAX**에 저장.

---

### 8. ArraySum 예시

```asm
ArraySum PROC USES esi ecx
  mov eax,0
L1:
  add eax,[esi]
  add esi,TYPE DWORD
  loop L1
  ret
ArraySum ENDP
```

* `USES` 키워드는 push/pop을 자동으로 생성하여 레지스터를 보호.

---

### 9. Link Library (링크 라이브러리)

* **링크 라이브러리**: 이미 컴파일된 프로시저들이 모인 파일.

  * `.obj` 파일들을 묶은 형태.
* **Dynamic Link Library (DLL)**: 실행 시 로드되는 라이브러리.

  * 예: `kernel32.dll`, `Irvine32.lib`

---

### 10. Irvine32 Library

초보자용 어셈블리 I/O 라이브러리.
Windows 환경에서 직접 OS 호출 없이 입출력을 수행.

#### 주요 함수

| 함수                        | 설명                  |
| ------------------------- | ------------------- |
| `Clrscr`                  | 화면 지우기              |
| `Delay`                   | 지정한 밀리초 동안 대기       |
| `DumpRegs`                | 레지스터 상태 출력          |
| `ReadInt`, `WriteInt`     | 정수 입력/출력            |
| `Random32`, `RandomRange` | 난수 생성               |
| `SetTextColor`            | 콘솔 글자색 변경           |
| `WriteString`, `Crlf`     | 문자열 출력, 줄바꿈         |
| `WaitMsg`                 | “아무 키나 누르세요” 메시지 표시 |

---

### 11. 예시 – 색상 출력

```asm
mov eax, yellow + (blue * 16)
call SetTextColor
mov edx, OFFSET str1
call WriteString
call Crlf
```

* 배경색은 곱하기 16, 전경색은 더하기로 지정.

---

### 12. 예시 – Random 출력

```asm
mov ecx,10
L1:
  mov eax,100
  call RandomRange
  call WriteInt
  call Crlf
  loop L1
```

---

### 13. Library Test 예시

* `TestLib1.asm`: 입력 후 DumpMem으로 메모리 표시.
* `TestLib2.asm`: 난수 생성 및 출력.
* `TestLib3.asm`: 루프 실행 시간 측정 (`GetMSeconds` 이용).

---

### 14. 요약

* **Stack**: 임시 저장, 인자 전달, 복귀 주소 저장.
* **Procedure**: 코드 재사용, 구조적 설계.
* **CALL/RET**: 흐름 제어 핵심.
* **USES**: 레지스터 자동 백업.
* **Irvine32 Library**: 편리한 입출력 인터페이스 제공.
