# Chapter 9 – Strings and Arrays

---

# 1. String Primitive Instructions (문자열 기본 명령)

## 1.1 문자열 명령 특징
- 기본 사용 레지스터: **ESI(소스), EDI(목적지)**  
- 누산기: **AL, AX, EAX**  
- Direction Flag(DF)에 따라 자동으로 주소 증가/감소한다.  
- REP prefix 사용 시 **ECX 카운터** 기반 반복 수행한다.

## 1.2 주요 명령
| 명령 | 설명 |
|------|------|
| MOVSB / MOVSW / MOVSD | ESI → EDI로 데이터 복사 |
| CMPSB / CMPSW / CMPSD | ESI와 EDI가 가리키는 값 비교 |
| SCASB / SCASW / SCASD | AL/AX/EAX의 값과 EDI의 메모리 비교 |
| STOSB / STOSW / STOSD | AL/AX/EAX 값을 EDI 위치에 저장 |
| LODSB / LODSW / LODSD | ESI 위치 값을 AL/AX/EAX로 로드 |

## 1.3 REP Prefix
- `REP`: ECX가 0이 될 때까지 반복  
- `REPE/REPZ`: ZF=1인 동안 반복  
- `REPNE/REPNZ`: ZF=0인 동안 반복

## 1.4 DF(방향 플래그)
- `CLD`: DF=0, 주소 증가  
- `STD`: DF=1, 주소 감소  

---

# 2. Irvine32 문자열 처리 함수

## 2.1 Str_compare
- 널 종료 문자열을 비교한다.  
- 대소문자 구분한다.  
- 결과 해석:
  - Carry=1 → string1 < string2  
  - Zero=1 → string1 == string2  
  - Carry=0 & Zero=0 → string1 > string2  

## 2.2 Str_length
- 문자열 길이를 EAX에 반환한다.
- 널 문자를 만날 때까지 1바이트씩 증가하며 계산한다.

## 2.3 Str_copy
- 소스 문자열을 대상 버퍼로 복사한다.  
- 대상 버퍼의 충분한 크기 필요.  
- REP MOVSB 기반 구현.

## 2.4 Str_trim
- 문자열 끝에서 특정 delimiter를 제거한다.
- 문자열 뒤에서 시작하여, delimiter가 아닌 문자를 발견하면 그 뒤에 널 문자 삽입한다.

## 2.5 Str_ucase
- 문자열의 모든 소문자를 대문자로 변환한다.
- 'a'~'z' 범위를 검사하여 대문자 비트를 적용한다.

---

# 3. Two-Dimensional Arrays (2차원 배열)

## 3.1 메모리 저장 방식
- **Row-major**: 행 단위로 연속 저장  
- **Column-major**: 열 단위로 연속 저장  

## 3.2 Base-Index addressing
- `[base + index]` 형태로 주소 계산  
- 2차원 배열 접근 시  
  - base = 행 오프셋  
  - index = 열 오프셋  

## 3.3 calc_row_sum 함수
- 특정 행의 byte 값들을 모두 더한다.
- `row_index * row_size`로 행 시작 주소를 계산한다.
- loop로 각 열을 순차 접근해 누적한다.

## 3.4 Scale factor
- WORD 배열: 2바이트 단위  
- DWORD 배열: 4바이트 단위  
- `TYPE` 연산자를 사용하면 자동 크기 반영 가능하다.

---

# 4. 정렬 및 탐색 알고리즘

## 4.1 Bubble Sort
- 인접 요소 두 개를 비교하여 큰 값을 뒤로 보낸다.
- 한 번의 pass 후 가장 큰 값이 배열 끝에 놓인다.
- Assembly 구현 특징:
  - `xchg`로 값 교환  
  - 이중 loop 사용  

## 4.2 Binary Search
- 정렬된 배열에서만 동작한다.
- mid = (first + last) / 2  
- 비교 결과에 따라 검색 구간을 절반으로 줄여나간다.
- Assembly 구현의 반환 규칙:
  - 찾으면 EAX = 해당 인덱스  
  - 못 찾으면 EAX = -1  

---

# 5. Chapter 핵심 정리

- 문자열 명령은 ESI/EDI 기반으로 자동 반복 및 인덱스 조정이 가능하다.  
- REP prefix와 DF 설정을 정확히 이해해야 한다.  
- Irvine32 문자열 함수는 실제 활용 가능한 문자열 처리 기능을 제공한다.  
- 2차원 배열은 주소 계산이 핵심이며 base-index-displacement를 자주 사용한다.  
- 정렬(Bubble Sort)과 탐색(Binary Search)의 어셈블리 구현은 반복 구조와 주소 연산 이해를 필요로 한다.
