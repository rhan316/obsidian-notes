
***Szybkie mnożenie i dzielenie przez potęgi dwójki**

Przesunięcia bitowe są wydajniejsze niż tradycyjne operacje arytmetyczne i mogą być używane do szybkiego mnożenia lub dzielenia przez potęgi liczby 2.
- Przesunięcie w lewo `<<` mnoży liczbę przez `2n (potęga n)`.
- Przesunięcie w prawo `>>` dzieli liczbę przez `2n (potęga n)`.
```
int x = 5; // Binary: 00000101
int result = x << 2; Przesunięcie w lewo o 2 bity: 00010100 (czyli 20)
(2 * 2 = 4) => 5 * 4 = 20

int y = 40; // Binary: 00101000
int divided = y >> 3; // Przesunięcie w prawo o 3 bity: 00000101 (czyli 5)
(2 * 2 * 2) => 40 / 8 = 5
```
Zastosowanie w wymagających algorytmach szybkich obliczeń np. w grafice komputerowej czy symulacjach fizycznych.


***Kompresja i dekompresja danych***

Przesunięcia bitowe pozwalają pakować wiele mniejszych wartości w jedną zmienną, co jest przydatne w ograniczonych środowiskach, np. w urządzeniach wbudowanych.
**Chcemy zapisać wiek (7 bitów), płeć (1bit) i stan (4 bity) w jednej zmiennej typu int**
```
int age = 25; // 7 bitów (0-127)
int gender = 1; // 1 bit (0=men, 1=woman)
int state = 10; // 4 bity (0-15)

// Kompresja
int packedData = (age << 5) | (gender << 4) | state;

// Odczyt danych
int exeAge = (packedData >> 5) & 0x7F; 
int exeGender = (packedData >> 4) & 0x1;
int exeState = packedData & 0xF;
```

***Szyfrowanie danych***

Przesunięcia bitowe są podstawowym elementem w algorytmach szyfrowania, takich jak XOR, gdzie sane są modyfikowane na poziomie bitu w celu ukrycia ich pierwotnego znaczenia.
```
int key = 0xA5;
int originalData = 0x3F;

// Szyfrowanie: 
int encryptedData = originalData ^ key; // 10011010 System.out.println("Zaszyfrowane: " + encryptedData);

// Deszyfrowanie: 
int decryptedData = encryptedData ^ key; // Powrót do 00111111 System.out.println("Odszyfrowane: " + decryptedData);
```