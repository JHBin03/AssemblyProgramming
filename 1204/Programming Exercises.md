1. mReadkey Macro  
ASCII 코드와 스캔 코드를 인자로 받아 ReadChar를 호출하여 키 입력을 기다린 후 ASCII와 스캔 코드를 각각 저장하도록 매크로를 작성한다.

---------
2. mWritestringAttr Macro  
문자열 주소와 색상을 인자로 받아 SetTextColor를 호출한 후 문자열을 출력하는 매크로를 작성한다.

---------
3. mMove32 Macro  
두 개의 32비트 메모리 피연산자를 인자로 받아 한쪽 값을 다른 쪽으로 이동하는 매크로를 작성한다.

---------
4. mMult32 Macro  
두 개의 32비트 메모리 피연산자를 곱하여 32비트 결과를 생성하는 매크로를 작성한다.

---------
5. mReadInt Macro  
16비트 또는 32비트 정수를 입력받아 크기에 맞게 결과를 저장하도록 조건 연산자를 사용하는 매크로를 작성한다.

---------
6. mWriteInt Macro  
부호 있는 정수를 출력하며 인자의 크기에 따라 byte, word, dword를 자동으로 처리하도록 조건 연산자를 사용하는 매크로를 작성한다.

---------
7. The Professor’s Lost Phone  
Drunkard’s Walk 프로그램을 수정하여 교수의 위치가 무작위 시간마다 변하고, 실행할 때마다 휴대폰이 다른 위치에서 분실되도록 시뮬레이션한다.

---------
8. Drunkard’s Walk with Probabilities  
이전 이동 방향을 유지할 확률 50%, 반대 방향 이동 확률 10%, 좌우 회전 확률 20%를 적용하여 Drunkard’s Walk 프로그램을 수정한다.

---------
9. Shifting Multiple Doublewords  
배열 이름, 방향, 시프트 비트 수를 인자로 받아 SHR 또는 SHL 명령으로 여러 개의 32비트 정수를 동시에 시프트하는 매크로를 작성한다.

---------
10. Three-Operand Instructions  
add3, sub3, mul3, div3 매크로를 작성하여 목적지 = source1 연산 source2 형태의 3피연산자 연산을 시뮬레이션한다.
