# Assembly Programming — Chapter 8

---

# 1. Stack Frame (스택 프레임)

## ✔ 정의

서브루틴 호출 시 스택 위에 생성되는 독립적 구조.

**포함 요소**

* 전달된 매개변수(parameters)
* return address
* 지역 변수(local variables)
* 저장된 레지스터(saved registers)

## ✔ 생성 과정 (p.2)

1. 인자 push
2. `call` → return address push
3. `push ebp`
4. `mov ebp, esp` (새로운 프레임 기준점)
5. `sub esp, n` (지역 변수 공간 확보)
6. 필요 레지스터 보존 (`push ebx`, `push ecx` …)

※ p.2 그림 — Stack Frame Creation Process

* Arguments → Return Address → Saved EBP → Local vars 순서로 쌓임.

---

# 2. 매개변수 전달 방식 (Passing Parameters)

## ✔ 2-1. 값 전달 (Value Passing) — p.5

* 단순 값의 복사본을 push
* 함수 내부에서 변경해도 원본 변수에 영향 없음
* 예: `AddTwo(val1, val2)`

## ✔ 2-2. 참조 전달 (Reference Passing) — p.6

* 변수의 **주소(offset)** 를 push
* 배열은 항상 참조로 전달됨
  예: `Swap(&a, &b)`

---

# 3. 스택 매개변수 접근 (Accessing Parameters)

## ✔ 기본 규칙 (p.7~8)

* `[ebp + 8]` : 첫 번째 인자
* `[ebp + 12]` : 두 번째 인자
* `[ebp + 4]` : return address
* `ebp` : 프레임 기준점

## ✔ Symbolic 이름 사용

```asm
x_param EQU [ebp+8]
y_param EQU [ebp+12]
```

---

# 4. Calling Conventions (스택 정리 방식)

## ✔ CDECL — 호출자(caller)가 정리 (p.10)

* 인자 push 순서: 오른쪽 → 왼쪽
* 정리: 호출자

  ```asm
  add esp, 8
  ```

## ✔ STDCALL — 피호출자(callee)가 정리 (p.11)

* `ret n` 사용
  예: `ret 8` → 파라미터 2개 정리

---

# 5. 레지스터 보존 (Saving & Restoring)

(p.12 예시 참고)

함수 내부에서 수정할 레지스터는
반드시 **push → pop** 해 복구해야 함.

예:

```asm
push ecx
push edx
...
pop edx
pop ecx
```

---

# 6. 지역 변수 (Local Variables)

## ✔ 생성 (p.13~14)

* EBP 아래쪽에 생성
* `sub esp, n` 으로 공간 확보

## ✔ 제거

```asm
mov esp, ebp
pop ebp
ret
```

p.14 그림에서는
EBP 아래에 X(EBP-4), Y(EBP-8) 같은 지역 변수가 위치함.

---

# 7. 참조 매개변수 활용 (Reference Parameters)

(p.15 ArrayFill 예시)

배열 주소 + 길이를 받아 내부에서 채우는 구조.

예:

```asm
mov esi, [ebp+12] ; 배열 주소
mov ecx, [ebp+8]  ; 길이
```

---

# 8. LEA 명령어 (Load Effective Address)

(p.16)

* 주소 계산용
* 문자열/배열 시작 주소 계산에 유용
* 메모리에 접근하지 않고 **주소 자체만 로드**

예:

```asm
lea esi, [ebp-30]
```

---

# 9. ENTER / LEAVE

## ✔ ENTER (p.17~18)

스택 프레임 생성 자동화

* `ENTER localSize, nestingLevel`

## ✔ LEAVE (p.19)

프레임 제거 자동화

```asm
mov esp, ebp
pop ebp
```

ENTER와 함께 사용할 것을 권장.

---

# 10. LOCAL 지시어 (p.20)

지역 변수를 이름으로 선언 가능:

```asm
LOCAL temp:DWORD, count:BYTE
```

---

# 11. 재귀 호출 (Recursion)

## ✔ 특징 (p.22~29)

* 반드시 **종료 조건** 필요
* 호출될 때마다 **새 스택 프레임** 생성됨

### ✔ CalcSum (p.23)

* ECX: 카운터
* 재귀가 언와인드될 때 EAX에 결과 누적

### ✔ Factorial (p.26~28)

* `n-1` push → recursive call
* 돌아오면서 `mul` 로 누적
* p.27~28 그림에서 재귀 스택 변화를 시각적으로 볼 수 있음.

---

# 12. INVOKE / ADDR / PROC / PROTO (p.30~45)

## ✔ INVOKE

* 인자 push
* CALL
* 규약에 맞게 스택 정리
  → **자동 처리 매크로**

```asm
INVOKE DumpArray, OFFSET array, LENGTHOF array, TYPE array
```

## ✔ ADDR

* INVOKE에서 주소 전달
* OFFSET과 달리 *메모리 변수의 주소 자체*를 넘김

## ✔ PROC

함수 정의

```asm
MyFunc PROC USES eax ebx,
    pNum:DWORD
```

## ✔ PROTO

함수 선언
다중 모듈에서 사용됨.

---

# 13. 멀티 모듈 프로그래밍 (p.46~52)

## ✔ 여러 .asm 파일 결합

* 각 모듈은 독립적으로 assemble
* 링크 단계에서 하나의 실행파일 생성

## ✔ 접근 제어

* `PUBLIC` : 외부 모듈에서 보임
* `PRIVATE` : 이 모듈 안에서만
* `OPTION PROC:PRIVATE` : 모든 PROC 기본 private

## ✔ 외부 함수 호출

* `EXTERN AddTwo@8 : PROC`
* @n 은 파라미터 크기 정보(바이트)

## ✔ EXTERNDEF

PUBLIC + EXTERN 기능을 동시에 수행.

---

# 14. StackFrame 출력 — WriteStackFrame (p.44~45)

Irvine32 제공:
현재 스택 프레임을 보기 좋게 출력해줌.

출력 내용:

* 매개변수
* return address
* 지역 변수
* 저장된 레지스터

---

# 15. Chapter Summary (p.55)

* Stack Frame 구조
* Pass by value / Pass by reference
* Calling conventions (cdecl / stdcall)
* Register save/restore
* Local variable allocation
* Recursion mechanics
* INVOKE / ADDR / PROC / PROTO
* Multi-module programming
* EXTERN / PUBLIC / PRIVATE
