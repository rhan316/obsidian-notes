**Głównym zadaniem procesora CPU** jest wykonywanie operacji na liczbach, ale nie w sensie matematycznym. Procesor operuje na danych, które są reprezentowane jako liczby w systemie binarnym, czyli za pomocą zer i jedynek. Te liczby mogą reprezentować różne rzeczy: od prostych wartości numerycznych po bardziej złożone struktury, takie jak adresy pamięci, instrukcje programu, znaki tekstowe, a nawet piksele obrazu.

### Jak procesor operuje na liczbach?

**Operacje arytmetyczne**
Procesor wykonuje podstawowe działania matematyczne, takie jak dodawanie, odejmowanie, mnożenie i dzielenie. Np. Jeśli masz dwie liczby `5` i `3`, procesor może je dodać, aby uzyskać wynik `8`.

**Operacje logiczne**
Procesor wykonuje operacje logiczne, takie jak `AND, OR, NOT, XOR`, które są używane do manipulacji bitami. Np. Jeśli masz liczby `5 -> (binarnie) 0101` i `3 -> 0011`, operacja `AND` da wynik `1 -> 0001`.

**Przenoszenie danych**
Procesor przenosi dane między pamięcią RAM, rejestrami i innymi komponentami systemu. Np. Procesor może załadować wartość z pamięci do rejestru, np. `EAX = 0x00401000`

**Sterowanie przepływem programu**
Procesor wykonuje instrukcje warunkowe (np. skoki), które decydują, która część kod ma zostać wykonana. Np. Jeśli wartość w rejestrze `EAX` jest równa zero, CPU może przeskoczyć do innej części programu.

**Praca z adresami pamięci**
Procesor oblicza adresy pamięci, aby odczytać lub zapisać dane. Np. Jeśli masz tablicę liczb, CPU oblicza adres konkretnego elementu, 
np. `adres = początek_tablicy + indeks * rozmiar_elementu`

### Dlaczego liczby są kluczowe?

Wszystko, co procesor robi, opiera się na liczbach, ponieważ:
- **Dane są reprezentowane jako liczby:** Tekst, obrazy, dźwięk, a nawet instrukcje programu są przechowywane w pamięci jako ciągi liczb binarnych.
- **Instrukcje są liczbami**: Każda instrukcja, którą wykonuje procesor, jest zakodowana jako liczba. Np. instrukcja dodawania może być reprezentowana przez kod `0x01`
- **Adresy pamięci to liczby**: Każde "pudełko" w pamięci RAM ma swój unikalny adres, który jest liczbą.

### Przykład jak procesor widzi świat
```java
// Załóżmy, że masz prosty program w Javie:
int a = 5;
int b = 3;
int c = a + b;
```
Procesor widzi to tak:
- Liczba `5` jest przechowywana w pamięci jako `00000101` (binarnie).
- Liczba `3` jest przechowywana w pamięci jako `0000011`.
- Procesor ładuje te wartości do rejestrów, np. `EAX = 00000101 (5)`, `EBX = 0000011 (3)`.
- Wykonuje operację dodawania: `EAX = EAX + EBX`, co daje wynik `8` .
- Zapisuje wynik z powrotem do pamięci.

