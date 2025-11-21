
## Liczby dodatnie w systemie binarnym

Komputer operuje na bitach (0 i 1), a liczby całkowite dodatnie są reprezentowane w systemie binarnym w sposób bezpośredni.

## Problem liczb ujemnych

Jak zapisać np. `-5` jako ciąg bitów?
Trzeba znaleźć sposób, by zakodować znak liczby.

### Uzupełnienie do dwóch (Two's Complement) - używane przez większość komputerów

Aby otrzymać liczbę ujemną:
- Weź binarną reprezentację liczby dodatniej.
- Zaneguj wszystkie bity.
- Dodaj `1`
#### Przykład `-5` w 8 bitach
```java
+5 = 00000101
Negacja: 11111010
Dodaj 1: 11111011
-5 = 11111011
```
