# 6장. Conditional Processing

## 💡 제어문의 내부 작동

고급 언어의 if, while 같은 제어문은 **비교(Comparison)** 와 **조건 분기(Conditional Jump)** 명령어로 구현된다.
CPU는 연산 결과에 따라 **플래그 레지스터(Flags Register)**의 비트를 설정(set) 또는 해제(clear)하며, 이 비트를 근거로 분기 명령을 수행한다.

---

## ⚙️ 플래그 비트 (Flag Bits)

| 플래그           | 의미      | 설명                    |
| ------------- | ------- | --------------------- |
| CF (Carry)    | 자리올림 발생 | unsigned 연산에서 오버플로 감지 |
| SF (Sign)     | 부호      | 연산 결과의 최상위 비트         |
| OF (Overflow) | 오버플로    | signed 연산에서 표현범위 초과   |
| PF (Parity)   | 패리티     | 결과의 1 비트 개수가 짝수면 1    |
| ZF (Zero)     | 제로      | 결과가 0이면 1             |

* **Overflow**: 비트 수가 허용하는 수를 넘었을 때
* **Underflow**: 그 반대 개념 (너무 작은 수)
* 대부분의 **비트 논리 연산(AND, OR, XOR, TEST)** 은 CF와 OF를 **항상 0으로 클리어**한다.

---

## 🔸 Boolean 연산 명령어

### 1️⃣ AND

* 특정 비트를 **지우는(clear)** 용도로 사용.
* **형식**: `AND dest, src`
* 예:

  ```asm
  AND AL, 00001111b  ; 하위 4비트만 남김
  ```
* **플래그 변화**: OF=0, CF=0, (SF, ZF, PF 수정)
* **문자 대소문자 변환 예시**:

  * `'A' = 41h`, `'a' = 61h` → 차이는 bit 5
  * `AND BYTE PTR [esi], 11011111b` → 소문자를 대문자로

---

### 2️⃣ OR

* 비트 합집합 (1이면 유지)
* **플래그 변화**: OF=0, CF=0, (SF, ZF, PF 수정)
* 예: 집합(Set) 표현에 사용 가능 — OR은 **합집합**, AND는 **교집합**.

---

### 3️⃣ XOR

* 서로 다른 비트면 1.
* **XOR 두 번 하면 원래 값 복원됨**:

  ```
  X XOR Y XOR Y = X
  ```
* **0을 1로 / 1을 0으로 반전**시킬 수 있음.
* 패리티 체크 시 `XOR reg, 0` 사용 (값 변경 없이 확인 가능)
* OF=0, CF=0 (SF, ZF, PF 수정)

---

### 4️⃣ NOT

* 비트 반전 (1의 보수)
* **플래그에 아무 영향 없음.**

---

### 5️⃣ TEST

* `AND`처럼 각 비트를 비교하지만, **결과를 저장하지 않음.**
* **형식**: `TEST dest, src`
* 플래그 변화: OF=0, CF=0 (SF, ZF, PF 수정)
* 예:

  ```asm
  TEST AL, 00100000b
  JNZ DeviceOffline
  ```

  → AL의 5번째 비트가 1이면 JNZ 분기 실행.

---

## 🔸 비교 명령어 (CMP)

* `CMP dest, src` → 내부적으로 `dest - src`를 계산하지만 **결과 저장 안 함.**
* 결과에 따라 플래그 설정:

  | 비교 결과      | ZF | CF |
  | ---------- | -- | -- |
  | dest < src | 0  | 1  |
  | dest > src | 0  | 0  |
  | dest = src | 1  | 0  |
* 이후 조건 분기(`JZ`, `JC`, `JG` 등)와 함께 사용.

---

## 🔸 조건 분기 (Conditional Jump)

* 조건이 참이면 지정된 레이블로 점프한다.
* 주요 명령어:

  | 명령어                 | 조건                      | 설명               |
  | ------------------- | ----------------------- | ---------------- |
  | JC / JNC            | Carry=1 / Carry=0       | 무부호 연산용          |
  | JZ / JNZ            | Zero=1 / Zero=0         | 같음 / 다름          |
  | JS / JNS            | Sign=1 / Sign=0         | 음수 / 양수          |
  | JO / JNO            | Overflow=1 / Overflow=0 | 오버플로 여부          |
  | JL / JG / JLE / JGE | 부호 있는 비교 결과             | less / greater 등 |

---

## 🔸 조건 루프 (Conditional Loop)

| 명령어             | 조건          | 설명            |
| --------------- | ----------- | ------------- |
| LOOPZ / LOOPE   | ZF=1인 동안 루프 | Zero일 때 반복    |
| LOOPNZ / LOOPNE | ZF=0인 동안 루프 | Nonzero일 때 반복 |
| LOOP            | ECX≠0일 때 루프 | 기본 반복         |

예시:

```asm
test WORD PTR [esi], 8000h ; 부호비트 검사
loopnz next
```

---

## 🔸 조건 구조 (Conditional Structures)

고급언어의 `if`, `while` 등을 **비교 + 분기 명령**으로 구현:

```asm
cmp eax, ebx
jg  greater_label
```

또는 MASM의 **고수준 제어 지시자** 사용 (32비트 한정):

```asm
.IF eax > val1
  mov result, 1
.ENDIF
```

→ 내부적으로 `CMP`, `JBE`, `MOV`로 변환됨.

---

## 🔸 예제 프로그램 요약

### 🔹 ArrayScan.asm

* 배열에서 첫 번째 **0이 아닌 값** 탐색
  `CMP [ebx], 0` → `JNZ found`

### 🔹 Encrypt.asm

* 문자열 암호화 (XOR 사용)

  ```asm
  XOR buffer[esi], KEY
  ```
* 같은 키로 XOR 두 번 하면 복호화됨.

### 🔹 ProcTable.asm

* 문자 입력(A–D)에 따라 **프로시저 테이블 호출**

  * 간접 호출(`CALL NEAR PTR [ebx + 1]`)로 다중 선택 구조 구현.

---

## 🧭 핵심 요약

* **AND / OR / XOR / NOT / TEST / CMP** → 조건 분기의 핵심
* **CF, ZF, SF, OF, PF** → 비교와 점프 판단 기준
* **Jcond** → 조건 분기 명령 (if-else 구현)
* **LOOPxx** → 반복 구조 구현
* **.IF / .ELSE / .ENDIF** → MASM 32bit 고수준 제어문
