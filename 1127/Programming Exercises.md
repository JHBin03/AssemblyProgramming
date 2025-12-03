# 9

1. Improved Str_copy Procedure  
    기존 Str_copy는 복사 길이를 제한하지 못하므로, 호출자가 최대 복사 가능 문자 수를 인자로 전달하도록 하여 해당 길이만큼만 복사하는 Str_copyN을 구현한다. ECX에 최대 복사 길이를 받고 REP MOVSB로 제한된 범위만 복사한다.
---
2. Str_concat Procedure  
    대상 문자열의 끝(null 위치)을 찾은 뒤, 소스 문자열의 문자를 순차적으로 이어 붙인다. 대상 문자열이 충분한 공간을 가지고 있어야 하며, 마지막에 null 문자를 추가한다.
---
3. Str_remove Procedure  
    문자열에서 특정 위치부터 n개의 문자를 삭제한다. 삭제 시작 위치 이후의 문자열을 앞으로 n칸 이동시키고 마지막에 null 문자를 다시 삽입하여 문자열을 정리한다.
---
4. Str_find Procedure  
    소스 문자열이 타겟 문자열 안에서 처음 발견되는 위치를 찾는 절차이다. 타겟 내 각 위치에서 소스 문자열과 문자 단위 비교를 수행하여 일치 시 Zero flag를 설정하고, EAX에 해당 위치 포인터를 반환한다. 찾지 못하면 Zero flag는 클리어된다.
---
5. Str_nextWord Procedure  
    문자열에서 지정된 delimiter 문자를 처음 찾고, 해당 delimiter를 null 문자로 교체한다. 발견 시 Zero flag가 설정되고 EAX는 delimiter 다음 문자 위치를 가리킨다. 발견하지 못하면 Zero flag는 클리어되고 EAX는 의미 없다.
---
6. Constructing a Frequency Table  
    문자열의 각 문자를 아스키 코드 값으로 해석하고, 해당 코드값을 인덱스로 하는 freqTable[256] 배열의 값을 1씩 증가시키며 등장 횟수를 센다. 문자열 전체를 순회한 후 빈도 테이블을 완성한다.
---
7. Sieve of Eratosthenes  
    2~65,000 범위의 소수를 찾기 위해 65,000개의 바이트 배열을 생성하고 모두 1로 초기화한다. 2부터 시작하여 현재 수의 배수 위치들을 0으로 설정한다. 배열에서 1로 남아 있는 위치가 소수이다.
---
8. Bubble Sort (exchange flag 사용)  
    BubbleSort 내부에서 값 교환이 발생할 때마다 exchange flag를 1로 설정한다. 한 회전(pass) 동안 교환이 한 번도 발생하지 않으면 정렬이 완료된 것이므로 조기 종료한다.
---
9. Binary Search 재작성  
    BinarySearch를 first, mid, last 값을 모두 레지스터로 유지하도록 다시 작성한다. 비교 후 탐색 범위를 절반으로 줄이며 레지스터 사용 규칙을 지키며 구현한다.
---
10. Letter Matrix  
    4×4 난수 문자 행렬을 생성하고, 각 문자가 50% 확률로 모음이 되도록 한다. 모든 행·열·대각선을 검사하여 4글자 조합을 만들고, 그중 모음이 정확히 2개 포함된 조합만 출력한다.
---
11. Letter Matrix/Sets with Vowels  
    앞의 문자 행렬을 기반으로 다시 4×4 행렬을 생성하여 각 문자에 50% 확률로 모음을 배치한다. 행·열·대각선에서 문자 집합을 만들어 모음이 정확히 2개 포함된 4글자 문자열만 출력한다.
---
12. Calculating the Sum of an Array Row  
    2차원 배열에서 특정 행의 합을 구하는 calc_row_sum 절차를 만든다. 인자로 배열 주소, 행 크기, 배열 유형(byte/word/dword), 행 인덱스를 받고 해당 행의 모든 값을 누적하여 EAX에 반환한다.
---
13. Trimming Leading Characters  
    문자열 맨 앞에서 특정 문자(delimiter)를 제거한다. 문자열 시작 위치부터 delimiter가 아닌 문자를 만날 때까지 인덱스를 증가시키고, 남은 문자열을 앞으로 복사하여 정리한다.
---
14. Trimming a Set of Characters  
    문자열 끝에서 여러 종류의 제거 문자 집합(filter set)을 기준으로 삭제 작업을 수행한다. 문자열 뒤에서 앞으로 이동하며 filter set에 속한 문자만 제거하고, 첫 비제거 문자를 만나면 그 뒤에 null을 삽입하여 정리한다.
---
