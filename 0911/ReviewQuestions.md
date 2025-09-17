# Review Questions
### 1. In an 8-bit binary number, which is the most significant bit (MSB)?
왼쪽 끝 비트 2^7 = 128
### 2. What is the decimal representation of each of the following unsigned binary integers?
- a. 00110101 = 53
- b. 10010110 = 150
- c. 11001100 = 204
### 3. What is the sum of each pair of binary integers?
- a. 10101111 + 11011011 = 110010010 (394)
- b. 10010111 + 11111111 = 110010110 (150)
- c. 01110101 + 10101100 = 100100001 (289)
### 4. Calculate binary 00001101 minus 00000111. 
13-7=6 -> 00000110
### 5.  How many bits are used by each of the following data types?
- a. word = 16
- b. doubleword = 32
- c. quadword  = 64
- d. double quadword =128
### 6. What is the minimum number of binary bits needed to represent each of the following unsigned decimal integers?
- a. 4095 -> 2^12 = 4096 > 4095 -> 12 bits
- b. 65534 -> 2^16 = 65536 > 65534 -> 16 bits
- c. 42319 -> 2^16 = 65536 > 42319 -> 16 bits
### 7. What is the hexadecimal representation of each of the following binary numbers?
- a. 0011 0101 1101 1010 -> 35DA
- b. 1100 1110 1010 0011 -> CEA3
- c. 1111 1110 1101 1011 -> FEDB
### 8. What is the binary representation of the following hexadecimal numbers?
- a. 0126F9D4 -> 0000 0001 0010 0110 1111 1001 1101 0100
- b. 6ACDFA95 -> 0110 1010 1100 1101 1111 1010 1001 0101
- c. F69BDC2A -> 1111 0110 1001 1011 1101 1100 0010 1010
### 9. What is the unsigned decimal representation of each of the following hexadecimal integers?
- a. 3A = 58
- b. 1BF = 447
- c. 1001 = 4097
### 10. What is the unsigned decimal representation of each of the following hexadecimal integers?
- a. 62 = 98
- b. 4B3 = 1203
- c. 29F = 671
### 11. What is the 16-bit hexadecimal representation of each of the following signed decimal integers?
- a. -24
- b. -311
### 12. What is the 16-bit hexadecimal representation of each of the following signed decimal integers?
- a. -21
- b. -45
### 13. The following 16-bit hexadecimal numbers represent signed integers. Convert each to decimal.
- a. 6BF9 = 27641
- b. C123 = -16066
### 14. The following 16-bit hexadecimal numbers represent signed integers. Convert each to decimal.
- a. 4CD2 = 19666
- b. 8230 = 32144
### 15. What is the decimal representation of each of the following signed binary numbers?
- a. 10110101 -> -76
- b. 00101010 -> 42
- c. 11110000 -> -16
  ### 16. What is the decimal representation of each of the following signed binary numbers?
- a. 10000000 → -128 (2의 보수 10000000 = -128)
- b. 11001100 → -52 (2의 보수: 00110100 + 1 = 00110101 = 53 → -53)
- c. 10110111 → -73 (2의 보수: 01001000 + 1 = 01001001 = 73 → -73)
### 17. What is the 8-bit binary (two’s-complement) representation of each of the following signed decimal integers?
- a. -1 → 11111111
- b. -128 → 10000000
- c. -33 → 11011111 (33 = 00100001 → 1의 보수: 11011110 + 1 = 11011111)
### 18. What is the 8-bit binary (two’s-complement) representation of each of the following signed decimal integers?
- a. -100 → 10011100 (100 = 01100100 → 1의 보수 10011011 + 1 = 10011100)
- b. -15 → 11110001
- c. -64 → 11000000
### 19. What is the sum of each pair of hexadecimal integers?
- a. 6B4 + 3FE = AB2
- b. A49 + 6BD = 10C6
### 20. What is the sum of each pair of hexadecimal integers?
- a. 7C4 + 3BE = B82
- b. B69 + 7AD = 1306
### 21. What are the hexadecimal and decimal representations of the ASCII character capital B?
- Hex: 42  
- Decimal: 66
### 22. What are the hexadecimal and decimal representations of the ASCII character capital G?
- Hex: 47  
- Decimal: 71
### 23. Challenge: What is the largest decimal value you can represent, using a 129-bit unsigned integer?
- 최대값: 2¹²⁹ − 1  
- 값: **680564733841876926926749214863536422911**
### 24. Challenge: What is the largest decimal value you can represent, using an 86-bit signed integer?
- 최대값: 2⁸⁵ − 1  
- 값: **478904856520590268236983445984471619071**  
  (양수 범위: −(2⁸⁵) ~ (2⁸⁵−1))
### 25. Create a truth table to show all possible inputs and outputs for the boolean function ¬(A ∨ B)

| A | B | A ∨ B | ¬(A ∨ B) |
|---|---|--------|-----------|
| 0 | 0 |   0    |     1     |
| 0 | 1 |   1    |     0     |
| 1 | 0 |   1    |     0     |
| 1 | 1 |   1    |     0     |
### 26. Create a truth table for (¬A ∧ ¬B). Compare to question 25.

| A | B | ¬A | ¬B | ¬A ∧ ¬B |
|---|---|----|----|---------|
| 0 | 0 |  1 |  1 |    1    |
| 0 | 1 |  1 |  0 |    0    |
| 1 | 0 |  0 |  1 |    0    |
| 1 | 1 |  0 |  0 |    0    |

- 결과 열은 문제 25와 동일함 → **드 모르간의 법칙** 증명됨:  
  - ¬(A ∨ B) ≡ ¬A ∧ ¬B
### 27. If a boolean function has four inputs, how many rows are required for its truth table?
- 2⁴ = **16 rows**
### 28. How many selector bits are required for a four-input multiplexer?
- 4개의 입력을 선택하려면: 2비트 필요 (2² = 4)  
→ **2 selector bits**
