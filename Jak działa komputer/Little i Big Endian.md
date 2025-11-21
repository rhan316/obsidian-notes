### Czym jest Endiannes?

Endiannes to sposób, w jaki komputer *układa bajty* wielobajtowej liczby (np. 16-bit, 32-bit, 64-bit) w pamięci.
##### Bity składają się na bajty, ale Endiannes określa kolejność bajtów, nie bitów!

#### Założenie
Weźmy przykład liczby 32-bitowej (czyli 4 bajty):
Hex: `0x12345678`

Podzał na bajty:
- bajt 1: `0x12`
- bajt 2: `0x34`
- bajt 3: `0x56`
- bajt 4: `0x78`

### BIG ENDIAN vs LITTLE ENDIAN

| Typ Endiannes | Kolejność bajtów w pamięci (adresy rosną) | Opis                                     |
| ------------- | ----------------------------------------- | ---------------------------------------- |
| Big Endian    | `12 34 56 78`                             | Najbardziej znaczący bajt (MSB) pierwszy |
| Little Endian | `78 56 34 12`                             | Najmniej znaczący bajt (LSB) pierwszy    |
### Przykład:

Liczba `0x12345678` (= 305419896 w systemie dziesiętnym)

#### W pamięci RAM:

| Adres | Big Endian | Little Endian |
| ----- | ---------- | ------------- |
| 0x00  | `0x12`     | `0x78`        |
| 0x01  | `0x34`     | `0x56`        |
| 0x02  | `0x56`     | `0x34`        |
| 0x03  | `0x78`     | `0x12`        |
***Czy bity w bajcie się zmieniają?***
Nie! Kolejność bitów w bajcie pozostaje taka sama. Endiannes dotyczy kolejności bajtów, nie samych bitów
### Gdzie to ma znaczenie?
- Sieci (TCP/IP) używają Big Endian (nazywane "network byte order")
- x86/Intel procesory -> używają Little Endian
- ARM -> obsługuje oba (ustawiane programowo)
- Problemy pojawiają się przy:
	- Przesyłaniu danych między systemami o różnych endianness
	- Odczycie plików binarnych lub pracy z niskopoziomowym C/C++

### Analogicznie
Wyobraź sobie zapisywanie liczby 1234:
- Big Endian: zapisz 1, potem 2, potem 3, potem 4.
- Little Endian: zapisz 4, potem 3, potem 2, potem 1.

Endianness dotyczy struktury danych, a nie wielkości plików.
Rozmiar pliku może wpływać na buforowanie, strukturę nagłówków, wydajność - ale nie na kolejność bajtów wewnątrz liczby.


