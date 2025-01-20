- **SOUNDEX**: Funkcja ta koduje tekst na podstawie jego wymowy, umożliwiając porównywanie słów o podobnym brzmieniu, nawet jeśli są zapisane różnie. Jest przydatna do wyszukiwania fonetycznych podobieństw, np. nazwisk w bazie danych, które mogą być zapisane z literówkami.
    
- **DIFFERENCE**: Porównuje dwa ciągi tekstowe na podstawie ich wartości SOUNDEX i zwraca liczbę od 0 do 4, gdzie 4 oznacza idealne dopasowanie. Używana do określania stopnia podobieństwa fonetycznego między dwoma słowami.
    

Są przydatne w sytuacjach, gdzie dane mogą zawierać błędy literowe lub fonetyczne różnice, np. przy wyszukiwaniu nazwisk, produktów czy miejscowości.

```
SELECT SOUNDEX('czerwony'); // C650
SELECT SOUNDEX('ciastko'); //  C232
Pierwsza litera jest zawsze taka sama, reszta jest wyliczana przez SQL dla danego słowa

SELECT DIFFERENCE('Postgres', 'Postgras'); // 4
Wynik tej funkcji to 4, co oznacza "perfekcyjne" dopasowanie

SELECT DIFFERENCE('czerwony', 'samochód'); // 0
Oznacza brak dopasowania
```