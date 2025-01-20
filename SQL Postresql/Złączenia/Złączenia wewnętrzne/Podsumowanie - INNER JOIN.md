Definicja => INNER JOIN łączy rekordy z dwóch (lub więcej) tabel tylko wtedy, gdy występuje dopasowanie w kolumnach w klauzuli ON.

Działanie => Zwraca wyłącznie wiersze, które spełniają warunek dopasowania (czyli rekordy, które mają wspólne wartości w określonych kolumnach)

Format podstawowy =>
```
SELECT
	tabelaX.kolumna, tabelaY.kolumna
FROM
	tabelaX
INNER JOIN
	tabelaY
ON
	tabelaX.wspólna_kolumna = tabelaY.wspólna_kolumna;
```
```
SELECT
	albums.Title AS "Album",
	tracks.Name AS "Tytuł"
FROM
	albums
INNER JOIN
	tracks
ON
	albums.AlbumId = tracks.AlbumId;
```

Kiedy używać INNER JOIN:
1. Łączenie powiązanych danych: Używaj, gdy potrzebujesz jedynie rekordów, które mają dopasowanie w obu tabelach (np. albumy z przypisanymi utworami).
2. Filtrowanie wyników: INNER JOIN eliminuje brakujące dopasowania - jeśli rekord nie ma odpowiadającego wiersza w drugie tabeli, nie znajdzie się w wyniku.

Zalety i Wady:
1. Wydajny przy dużych zbiorach danych, bo zwraca tylko dopasowane rekordy.
2. Pomija dane bez dopasowania; jeśli zależy Ci na pełnym przeglądzie danych z jednej tabeli (nawet bez dopasowań), INNER JOIN nie będzie właściwym wyborem (lepszy będzie LEFT JOIN)
