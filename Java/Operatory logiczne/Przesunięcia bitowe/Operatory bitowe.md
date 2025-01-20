Operatory bitowe w Javie pozwalają na manipulację danych na poziomie bitów. Są wydajne i często stosowane w zaawansowanych algorytmach, gdzie operacje na bitach są kluczowe.


| Operator | Opis               | Wynik na poziomie bitów                       |
| -------- | ------------------ | --------------------------------------------- |
| `&`      | AND                | Zwraca 1, jeśli oba bity to 1                 |
| \|       | OR                 | Zwraca 1, jeśli przynajmniej jeden bit to 1   |
| ^        | XOR (Exclusive OR) | Zwraca 1, jeśli oba bity są różne             |
| ~        | NOT (negacja)      | Neguje każdy bit (zmienia 1 na 0 i odwrotnie) |
```
a = 5 binarnie: 0101
b = 3 binarnie: 0011

OPERACJE:

AND (&)
	0101 & 0011 = 0001 (wynik: 1)
OR (|)
	0101 | 0011 = 0111 (wynik 7)
XOR (^)
	0101 ^ 0011 = 0110 (wynik 6)
NOT (~)
	~0101 = 1010 (w systemie uzupełnienia do 2 = -6)
```