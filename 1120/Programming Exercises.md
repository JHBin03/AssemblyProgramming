# Programming Exercises

1. FindLargest Procedure  
Create a procedure named FindLargest that receives a pointer to a signed doubleword array and a count of the array’s length. Return the largest value in EAX.
답:  
배열 주소([ebp+8])와 길이([ebp+12])를 받아 전부 순회하며 가장 큰 값을 비교해 EAX에 저장해 반환한다.  
PROTO 선언과 여러 테스트 배열을 호출하는 main 프로그램을 작성해야 한다.

---
2. Chess Board  
Write a program that draws an 8×8 chess board using alternating gray and white squares.
답:  
Irvine32의 SetTextColor와 Gotoxy를 활용해 8×8 반복문으로 칸 색을 번갈아 출력한다.  
전역 변수를 사용하지 않고, 절차별로 분리된 PROC 구조를 사용한다.

---
3. Chess Board with Alternating Colors  
Every 500ms마다 색을 변경하며 보드를 총 16번 다시 그린다. 흰 칸은 항상 유지한다.
답:  
Exercise 2를 기반으로 500ms 딜레이(loop 또는 Delay 함수) 후 색 변경 로직을 추가하여 16회 반복 출력한다.

---
4. FindThrees Procedure  
Return 1 if an array has three consecutive values of 3, otherwise return 0.
답:  
배열 주소([ebp+8])와 길이([ebp+12])를 받아 인접한 세 요소가 모두 3인지 검사하여 맞으면 EAX=1, 아니면 0을 반환하는 PROC을 만든다.

---
5. DifferentInputs Procedure  
Return EAX=1 if the three input parameters are all different; otherwise EAX=0.
답:  
세 값([ebp+8], [ebp+12], [ebp+16])이 모두 서로 다른지 비교하고, 모두 다르면 EAX=1, 아니면 0을 반환한다.  
PROTO 선언 포함, 테스트 프로그램에서 서로 다른 입력으로 5회 호출한다.

---
6. Exchanging Integers  
Using the Swap procedure from Section 8.4.6, create an array of random integers and swap each consecutive pair.
답:  
무작위 배열 생성 후 Swap PROC을 반복 호출하여 0–1, 2–3, 4–5 … 순서로 쌍 교환을 수행한다.

---
7. Greatest Common Divisor  
Write a recursive implementation of Euclid’s GCD algorithm.
답:  
입력 두 값이 [ebp+8], [ebp+12]에 전달되며 n2=0일 때 n1 반환, 그렇지 않으면 GCD(n2, n1 mod n2)를 재귀 호출한다.  
주어진 다섯 쌍 (5,20), (24,18), (11,7), (432,226), (26,13)을 사용해 각 호출 후 결과 출력한다.

---
8. Counting Matching Elements  
CountMatches receives two pointers to arrays and a length. Count matching indices where x[i] == y[i].
답:  
pA=[ebp+8], pB=[ebp+12], count=[ebp+16]을 받아 x[i] == y[i]일 때 카운트를 증가시키고 최종 결과를 EAX에 저장한다.  
레지스터 보존 규칙을 지키며 PROTO 선언을 포함한다.

---
9. Counting Nearly Matching Elements  
CountNearMatches receives two arrays, a length, and a maximum allowed difference.  
Count when |x[i] - y[i]| ≤ diff.
답:  
pA, pB, count, diff 총 네 개 인자를 받아 각 요소의 차이가 diff 이하인지 검사해 조건을 만족할 때마다 카운터를 증가시키고 EAX로 반환한다.

---
10. Show Procedure Parameters  
ShowParams displays each 32-bit parameter in order from lowest to highest address, both decimal and hex.
답:  
파라미터 개수 paramCount를 받아 [ebp+8], [ebp+12], [ebp+16] …을 순차적으로 읽어 주소와 값을 출력한다.  
MySample에서 세 파라미터를 전달 후 ShowParams paramCount 형태로 호출한다.
