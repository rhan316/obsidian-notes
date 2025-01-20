Redis oferuje różnorodne struktury danych, które pozwalają efektywnie przechowywać i manipulować danymi w pamięci.

***Strings*** Najprostsza i najbardziej podstawowa struktura danych w Redis. Przechowuje ciąg znaków lub binarne wartości o maksymalnym rozmiarze 512 MB.
Przykładowe polecenia:
	Ustawienie wartości `SET key value`
	Pobieranie wartości `GET key`
	Inkrementacja liczby `INCR key`
	Dodanie wartości `APPEND key value`
Zastosowanie:
	Przechowywanie tokenów sesji.
	Liczniki, np. liczba odwiedzin strony.

**Lists** Kolekcja uporządkowanych ciągów znaków. Działa jak lista w językach programowania.
Przykładowe polecenia:
	Dodanie elementu na początku: `LPUSH key value`
	Dodanie elementu na końcu: `RPUSH key value`
	Pobranie zakresu elementów: `LRANGE key start stop`
	Usunięcie i pobranie pierwszego elementu: `LPOP key`
Zastosowanie:
	Implementacja kolejek FIFO.
	Przechowywanie historii zdarzeń.

