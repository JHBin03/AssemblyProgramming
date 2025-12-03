# 9

1. Which Direction flag setting causes index registers to move backward through memory when executing string primitives?
    DF가 1(설정됨)일 때 인덱스 레지스터가 감소하여 메모리를 역방향으로 이동한다. 즉, STD 명령으로 DF가 설정된 상태이다.
---
2. When a repeat prefix is used with STOSW, what value is added to or subtracted from the index register?
    STOSW는 2바이트 저장 명령이므로 DF가 0이면 EDI가 +2 증가하고, DF가 1이면 EDI가 -2 감소한다.
---
3. In what way is the CMPS instruction ambiguous?
    CMPS는 비교 후 어떤 값이 더 큰지에 대한 정보가 플래그로만 남기 때문에, 실제 비교 대상이 ESI 쪽인지 EDI 쪽인지 코드 문맥을 모르면 의미가 모호하다.
---
4. When the Direction flag is clear and SCASB has found a matching character, where does EDI point?
    SCASB는 비교 후 EDI를 자동 증가시키므로, 매칭을 발견하면 EDI는 ‘일치한 문자 다음 위치’를 가리키게 된다.
---
5. When scanning an array for the first occurrence of a particular character, which repeat prefix would be best?
    REPE(또는 REPZ)가 가장 적합하다. 일치할 때까지 반복하며 조건이 깨질 때 멈추기 때문이다.
---
6. What Direction flag setting is used in the Str_trim procedure from Section 9.3?
    Str_trim은 문자열 끝에서 앞으로 스캔하지 않고, 내부에서 포인터 이동을 수동으로 처리하므로 DF는 기본적으로 CLD(DF=0, 증가 방향) 상태를 사용한다.
---
7. Why does the Str_trim procedure from Section 9.3 use the JNE instruction?
    JNE는 현재 문자가 제거 대상(delimiter)이 아닐 때 루프를 종료하기 위해 사용된다. 즉, delimiter가 아닌 문자를 발견하면 JNE로 빠져나온다.
---
8. What happens in the Str_ucase procedure from Section 9.3 if the target string contains a digit?
    숫자는 ‘a~z’ 범위가 아니므로 변환 조건에 해당하지 않고 그대로 유지된다.
---
9. If the Str_length procedure from Section 9.3 used SCASB, which repeat prefix would be most appropriate?
    REPNE(또는 REPNZ)가 적합하다. 널 문자(0)를 찾을 때까지 반복해야 하기 때문이다.
---
10. If the Str_length procedure from Section 9.3 used SCASB, how would it calculate and return the string length?
    SCASB를 REPNE와 함께 사용하면, EDI가 널 문자를 지나간 위치를 가리킨다.  
    문자열 길이는 (종료 위치 - 시작 위치 - 1) 또는 반복 횟수(ECX의 감소량)로 계산할 수 있다.
---
11. What is the maximum number of comparisons needed by the binary search algorithm when an array contains 1,024 elements?
    이진 탐색의 최대 비교 횟수는 log2(1024) = 10회이다.
---
12. In the FillArray procedure from the Binary Search example in Section 9.5, why must the Direction flag be cleared by the CLD instruction?
    메모리를 순방향(증가 방향)으로 초기화해야 하므로 DF가 반드시 0이어야 한다.  
    DF가 1이면 ESI/EDI가 감소하여 잘못된 메모리 방향으로 접근하게 되므로, CLD로 DF를 0으로 설정해야 한다.
---
