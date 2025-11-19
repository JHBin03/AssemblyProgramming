# Programming Exercises

1. Display ASCII Decimal  
답:  
EDX에 숫자 주소, ECX에 길이, EBX에 소수점 위치를 전달한 뒤  
오른쪽에서 EBX만큼 왼쪽 위치에 '.' 문자를 삽입해 문자열을 출력한다.  
실제로는 숫자를 한 글자씩 읽으며 출력 인덱스가 (길이-EBX)에 도달했을 때 '.'을 출력하는 방식으로 구현하면 된다.
----
2. Extended Subtraction Procedure  
답:  
길이가 같은 두 이진수를 끝에서부터 SBB로 빼며 carry(빌림)를 처리한다.  
각 바이트 또는 워드를 뒤에서 앞으로 SBB 한 후 결과 배열에 저장하는 구조로 절차를 구현한다.
----
3. Packed Decimal Conversion  
답:  
4바이트 packed decimal(각 nibble = 10진수)을 상위 nibble → 하위 nibble 순으로 분리하여  
각 nibble에 30h를 더해 ASCII 문자로 변환해 버퍼에 저장한다.
----
4. Encryption Using Rotate Operations  
답:  
key 배열의 각 값만큼 평문 바이트를 ROL 또는 ROR 한다.  
음수 key → ROR, 양수 key → ROL.  
처음 10바이트는 key[0~9] 적용, 그 다음 10바이트는 key[0~9] 다시 반복 적용하여 전체 메시지 암호화.
----
5. Prime Numbers  
답:  
에라토스테네스의 체 실행: 2~1000 배열을 만든 뒤  
배수들을 제거하며 남은 숫자만 출력한다.
----
6. Greatest Common Divisor (GCD)  
답:  
x = |x|, y = |y| 적용 후  
do  
    n = x mod y  
    x = y  
    y = n  
while(y > 0)  
return x  
이 로직을 그대로 idiv와 레지스터 교환을 통해 구현한다.
----
7. Bitwise Multiplication  
답:  
32비트 unsigned 값 EBX를 EAX에 곱하는 과정에서  
곱셈(MUL) 없이,  
(1) EBX의 최하위 비트 검사  
(2) 1이면 EAX를 결과에 ADD  
(3) EBX는 SHR 1  
(4) EAX는 SHL 1  
이 과정을 EBX의 모든 비트가 처리될 때까지 반복한다.
----
8. Add Packed Integers  
답:  
각 packed integer(4바이트, 8바이트, 16바이트 등)를 뒤에서부터  
DAA 또는 ADC를 사용해 자릿수별로 더하고 carry를 다음 자리로 전달한다.  
EAX=숫자 수, EBX=길이, ESI=첫 숫자 주소, EDI=두 번째 숫자 주소를 참조하며  
각 자리 nibble을 더해 packed decimal 결과를 만든다.
