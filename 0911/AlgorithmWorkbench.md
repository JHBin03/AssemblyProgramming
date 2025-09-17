# Algorithm Workbench
### 1. Write a function that receives a string containing a 16-bit binary integer. The function must return the string’s integer value.
- **풀이:**  
  16자리 이진수 문자열을 받아서 각 자리의 비트를 2의 거듭제곱으로 곱해 더한다.  
  예: "0000000000001010" → 10
### 2. Write a function that receives a string containing a 32-bit hexadecimal integer. The function must return the string’s integer value.
- **풀이:**  
  16진수 문자열을 각 자리의 값을 16의 거듭제곱으로 곱해 더한다.  
  예: "0000001A" → 26
### 3. Write a function that receives an integer. The function must return a string containing the binary representation of the integer.
- **풀이:**  
  정수를 2로 나눈 나머지를 역순으로 배열해 2진수 문자열 생성.
### 4. Write a function that receives an integer. The function must return a string containing the hexadecimal representation of the integer.
- **풀이:**  
  정수를 16으로 나눈 나머지를 역순으로 배열해 16진수 문자열 생성.
### 5. Write a function that adds two digit strings in base b, where 2 ≤ b ≤ 10. Each string may contain as many as 1,000 digits. Return the sum in a string that uses the same number base.
- **풀이:**  
  두 문자열을 끝자리부터 한 자리씩 더하며 자리올림 처리.  
  자리올림이 있으면 다음 자리 더하기에 포함.
### 6. Write a function that adds two hexadecimal strings, each as long as 1,000 digits. Return a hexadecimal string that represents the sum of the inputs.
- **풀이:**  
  5번과 동일 원리, 단 16진수이므로 0-9, A-F 문자를 숫자로 변환 후 덧셈, 자리올림 처리.
### 7. Write a function that multiplies a single hexadecimal digit by a hexadecimal digit string as long as 1,000 digits. Return a hexadecimal string that represents the product.
- **풀이:**  
  단일 16진수 숫자와 16진수 문자열을 끝자리부터 곱하며 자리올림 처리.  
  곱셈 결과를 16진수 문자열로 변환해 반환.
