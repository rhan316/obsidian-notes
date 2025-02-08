Użycie znaku z dużej lub małej litery ma znaczenie! 
Np. użycie m oznacza minutę, a M oznacza miesiąc.
Użycie więcej niż 1 znaku również ma znaczenie:
M --> 1
MM --> 01
MMM --> Jul
MMMM --> July (full)

| Symbol | Znaczenie        | Przykład                   |
| ------ | ---------------- | -------------------------- |
| y      | Year             | 20, 2025                   |
| M      | Month            | 1, 01, Jan, January        |
| d      | Day              | 5, 05                      |
| h      | Hour             | 0, 09                      |
| m      | Minute           | 45                         |
| s      | Second           | 52                         |
| a      | a.m/p.m          | AM, PM                     |
| z      | Time Zone Name   | Eastern Standard Time, EST |
| Z      | Time Zone Offset | -0400                      |
```
Jeśli chcemy dodać dodatkowy tekst do daty, godziny to używamy pojedynczych cudzysłów
Np. DateTimeFormatter.ofPattern("'Data:' dd MMMM yyyy 'Godzina:' hh:mm");
```