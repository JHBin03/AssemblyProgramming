# 7. Integer Arithmetic
---

## 1. Shift & Rotate (비트 이동 / 회전)

###  Logical Shift
- **SHL**: 왼쪽으로 쉬프트. LSB에는 0이 들어감.
- **SHR**: 오른쪽으로 쉬프트. MSB에는 0이 들어감.

###  Arithmetic Shift
- **SAL**: SHL과 동일.
- **SAR**: 오른쪽 산술 쉬프트. 최상위 비트(MSB, 부호 비트)를 유지해 부호 보존.

###  Rotate
- **ROL**: 왼쪽 회전. 최상위 비트 → CF, LSB 위치로 이동.
- **ROR**: 오른쪽 회전. 최하위 비트 → CF, MSB 위치로 이동.
- **RCL / RCR**: Carry flag까지 포함하여 회전.

###  Double-Precision Shift
- **SHLD**: 왼쪽 더블 쉬프트. 빈 칸을 source의 상위 비트로 채움.
- **SHRD**: 오른쪽 더블 쉬프트. 빈 칸을 source의 하위 비트로 채움.

---

## 2. Shift & Rotate 활용

###  배열 비트 쉬프트
배열 전체를 1bit 오른쪽으로 쉬프트하는 단계적 절차 소개.

###  Binary → ASCII 변환 (`BinToAsc`)
Carry flag를 이용해 32-bit 정수를 ASCII 이진 문자열로 변환하는 코드 예시 포함.

---

## 3. Multiplication & Division (곱셈/나눗셈)

###  MUL (unsigned)
- 피연산자 크기 동일.
- 결과는 *두 배 크기*의 레지스터에 저장.
- 상위 절반이 0인지 확인하려면 Carry flag 검사.

###  IMUL (signed)
- **1-operand**: AX, DX:AX, EDX:EAX에 저장.
- **2/3-operand**: destination 크기로 잘림 → Overflow/Carry 플래그로 손실 여부 확인.

###  DIV / IDIV
- 8비트 DIV 전에는 **AX를 완전한 부호 확장** 해야 함.
- 나눗셈 결과가 destination에 못 들어가면 divide overflow → 프로그램 예외.
- **Division by zero 방지**: 항상 피제수(divisor)를 검사할 것.

---

## 4. Sign Extension (부호 확장)

### 확장 규칙:
- byte → word
- word → doubleword
- doubleword → quadword

부호 있는 값은 sign bit를 이용하여 확장해야 실제 계산 결과가 맞게 처리됨.

---

## 5. Extended Addition & Subtraction

###  ADC (Add with Carry)
Carry flag까지 포함하여 더함.  
멀티-정밀도 연산(큰 정수 덧셈)에 사용.

###  SBB (Subtract with Borrow)
Carry flag를 포함하여 뺌.

---

## 6. ASCII & Unpacked Decimal Arithmetic

### 특징
- Unpacked decimal은 상위 4bit가 0000b.
- ASCII 숫자는 상위 4bit가 항상 0011b (즉, 30h offset).

### 주요 명령어
- **AAA**: ADD 후 ASCII 조정
- **AAS**: SUB 후 ASCII 조정
- **AAM**: MUL 결과를 unpacked decimal로 조정
- **AAD**: DIV 전에 ASCII → binary 변환

---

## 7. Packed Decimal Arithmetic (DAA/DAS)

###  DAA (Addition)
ADD/ADC 이후 AL에 있는 값을 packed decimal 형태로 조정.

###  DAS (Subtraction)
SUB/SBB 이후 AL을 packed decimal 형태로 조정.

---

## 8. Chapter Summary
- Shift/Rotate 종류 및 플래그 변화
- MUL/IMUL의 방식 차이 및 overflow 처리
- DIV/IDIV의 부호 확장 규칙
- BCD 연산과 ASCII/packed decimal 조정 명령어
- 확장 산술(ADC/SBB)의 멀티정밀도 활용
