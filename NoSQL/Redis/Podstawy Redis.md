~={red}**Redis (Remote Dictionary Server)**=~ to baza danych NoSQL, która jest wyjątkowa, ponieważ działa głównie w pamięci (RAM). Oznacza to, że jest szybka jak błyskawica, co czyni ją idealną do zastosowań, gdzie kluczowa jest wydajność, takich jak cache, kolejkowanie zadań czy sesje użytkownika.
~={8}
**Klucz - Wartość (Key-Value Store)**=~
Redis jest bazą typu klucz-wartość, co oznacza, że dane przechowujesz w parach, podobnie jak w słowniku (mapie) w Javie:
- *Klucz* to unikalny identyfikator (np. user123).
- *Wartość* to dane, które mogą być w różnych formatach: liczby, ciągi znaków, listy, hashe, zestawy(sets), a nawet struktury przestrzenne.
*Analogia* -> Wyobraź sobie, że Redis to szafa z tysiącem szuflad. Każda szuflada ma unikalną etykietę(klucz), a w środku możesz przechowywać różne rzeczy(wartość): dokumenty, pudełka z rzeczami(listy), czy katalogi (hashe).

~={8}**Dane w pamięci RAM**=~
Redis przechowuje dane głównie w pamięci RAM, co sprawia, że operacje są nawet *setki razy szybsze* niż w tradycyjnych bazach danych opartych na dyskach.
*Analogia* -> Wyobraź sobie notatnik na biurku (Redis), który pozwala Ci błyskawicznie zapisać i odczytać dane, zamiast sięgać do archiwum w piwnicy (tradycyjna baza SQL na dysku).

~={8}**Struktury danych Redis**=~
1. **String (ciągi znaków)**: Najprostsza forma danych. Może to być liczba, tekst, JSON itp. `SET klucz "wartość"` -> zapisuje wartość. `GET klucz` odczytuje wartość na podstawie klucza.
2. **Listy: kolekcje uporządkowane, jak ArrayList w Javie**: `LPUSH lista "a"` -> dodaje "a" na początek. `LRANGE lista 0 -1` -> pobiera całą listę.
3. **Hash'e**: Zbiory klucz-wartość, jak mapa Map<K, V>. Zapis: `HSET user:1 name "Jan" age 30`. Odczyt: `HGETALL user:1`.
4. **Zbiory (Sets), nieuporządkowane kolekcje unikalnych wartości**: `SADD set "a", "b", "C"`. Odczyt: `SMEMBERS set`.
5. **Zbiory uporządkowane (Sorted Sets) - zbiory z przypisanymi rankingami**. `ZADD rank 100 "user"`. Odczyt `ZRANGE rank 0 -1 WITHSOCRES`.

**Trwałość danych**
Choć Redis działa w pamięci RAM, może także zapisywać dane z dysku, aby nie stracić ich przy restarcie:
1. ~={green}**RDB (Redis Database Backup)**=~: Okresowy snapshot danych.
2. ~={blue}**AOF (Append Only File)**:=~ Zapisuje każdą operację, aby odtworzyć stan bazy.
*Analogia:* Wyobraź sobie to jak robienie zdjęcia szafy (RDB) lub zapisywanie każdego ruchu, który wykonujesz przy otwieraniu lub zamykaniu szuflad.

***Typowe zastosowania Redis***
- **Cache (pamięć podręczna)** - Redis jest często używany jako pamięć podręczna dla danych, które są kosztowne w generowaniu (np. wyniki zapytań do bazy danych).
- **Sesje użytkownika** - Przechowywanie danych sesji użytkownika w Redis jest powszechną praktyką w aplikacjach webowych.
- **Kolejki zadań** - Redis List i Stream mogą być używane jako kolejki do przetwarzania zadań.
- **Ranking (leaderboards)** - Dzięki Sorted Sets Redis jest idealny do zarządzania rankingami w grach lub aplikacjach społecznościowych.
- **Zliczanie i analityka** - Redis obsługuje licznik i operacje na dużych danych, co czyni go idealnym do analityki.


