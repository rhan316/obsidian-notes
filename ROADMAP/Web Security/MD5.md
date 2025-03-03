**MD5 (Message Digest Algorithm 5)** to algorytm skrótu kryptograficznego, który przekształca dowolne dane wejściowe w 128-bitowy hash. Jest często stosowany do sprawdzenia integralności danych, ale *nie jest zalecany do przechowywania haseł* w aplikacjach Spring Boot ze względów bezpieczeństwa.

### Jak działa algorytm MD5?
MD5 to algorytm, który bierze dane wejściowe i tworzy z nich 128-bitowy skrót (hash).

**Przygotowanie danych (Padding)**
Dane wejściowe są uzupełniane tak, aby ich długość była wielokrotnością 512 bitów (64 bajtów).
Do końca wiadomości dodawana jest jedynka `1`, a potem zera `0`.
Ostatnie 64 bity zawierają długość oryginalnej wiadomości.

**Inicjalizacja 4 rejestrów (A, B, C, D)**
MD5 używa czterech 32-bitowych rejestrów, które są inicjalizowane następującymi wartościami heksadecymalnymi:
```ini
A = 0x67452301
B = 0xEFCDAB89
C = 0x98BADCFE
D = 0x10325476
```

**Przetwarzanie bloków po 512 bitów**
Każdy blok jest dzielony na 16 słów na 32 bity.
Algorytm wykonuje 64 rundy przekształceń z wykorzystaniem funkcji nieliniowych i przesunięć bitowych.
Każda runda wykorzystuje różne stałe `T[i]` i operacje takie jak:
`AND, OR, XOR, NOT`, Rotacje bitowe (left rotate).

**Łączenie wyników**
Po przejściu przez wszystkie bloki wartości `(A, B, C, D)` są dodawane do początkowych wartości rejestrów.
Wynik jest konwertowany na ciąg heksadecymalny (16 bajtów = 32 znaki hex).
###  Dlaczego MD5 jest niebezpieczny?
MD5 był kiedyś popularny, ale obecnie jest uznawany za podatny na ataki:
- *Ataki kolizyjne* - można znaleźć różne wejścia prowadzące do tego samego hasha.
- *Szybkie obliczenia* - istnieją ogromne bazy danych "rainbow tables", które pozwalają szybko odwrócić MD5 do oryginalnego tekstu.
- *Brak soli* - MD5 nie dodaje losowego elementu do wartości przed hashowaniem, co czyni go jeszcze bardziej podatnym na ataki.

**Bezpieczne alternatywy w Spring Boot**
W SB do przechowywania haseł *zawsze należy używać mocniejszych algorytmów jak:*
- `BCrypt` - domyślna opcja w Spring Boot `BCrpytPasswordEncoder`
- `PBKDF2` - używa wielu iteracji, co spowolnia ataki brute-force
- `Argon2` - nowoczesny algorytm zoptymalizowany pod kątem bezpieczeństwa

