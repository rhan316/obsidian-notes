Rejestry w SHA to zbiór zmiennych 32-bitowych lub 64-bitowych, które są wykorzystywane do przechowywania pośrednich wyników podczas obliczania hasha. Można je traktować jak pamięć roboczą algorytmu, gdzie przechowywane są tymczasowe dane w trakcie mieszania (tzw. "compression function").
Każda wersja SHA ma swój własny zestaw rejestrów początkowych (inicjalizowanych stałymi wartościami) oraz rejestrów używanych podczas obliczeń.

### Rejestry w SHA-256
SHA-256 używa 8 32-bitowych rejestrów, które są inicjalizowane na początku działania algorytmu stałymi wartościami heksadecymalnymi:

| Rejestr | Wartość początkowa (hex) |
| ------- | ------------------------ |
| A       | `0x6a09e667`             |
| B       | `0xbb67ae85`             |
| C       | `0x3c6ef372`             |
| D       | `0xa54ff53a`             |
| E       |                          |
| F       |                          |
| G       |                          |
| H       |                          |
