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
| E       | `0x510e527fade682d1`     |
| F       | `0x9b05688c2b3e6c1f`     |
| G       | `0x1f83d9abfb41bd6b`     |
| H       | `0x5be0cd19137e2179`     |
SHA-512 przetwarza 1024-bitowe bloki i używa 80 rund, ale mechanizm rejestrów pozostaje ten sam.

- Rejestry w SHA przechowują stan pośrednich obliczeń i są aktualizowane w każdej rundzie.
- SHA-256 ma osiem 32-bitowych rejestrów. SHA-512 ma 8 64-bitowych rejestrów.
- Operacje na rejestrach obejmują funkcje logiczne i przesunięcia bitowe, aby zapewnić mieszanie danych.
- Na końcu działania algorytmu wartości rejestrów są łączone, tworząc finalny hash.

