BitMapa przypomina strukturę taką jak `Map<Integer, Boolean>`, ponieważ jej celem jest przypisywanie pewnego stanu `true/false` do elementu identyfikowanego przez index (klucz Integer). Jednak BitMapa różni się znacząco pod względem ~={8}wydajności i zużycia pamięci=~.

*Porównanie BitMapy do Map<Integer, Boolean>*

| Cechy                 | BitMapa                               | Map<Integer, Boolean>                                |
| --------------------- | ------------------------------------- | ---------------------------------------------------- |
| Pamięć                | Bardzo efektywna: 1 bit na element    | Każdy klucz i wartość zajmują dużo więcej pamięci    |
| Szybkość operacji     | Operacje w czasie stałym `O(1)`       | Zależnie od implementacji mapy `O(log n)` lub `O(1)` |
| Obsługa dużych danych | Klucze muszą być liczbami całkowitymi | Klucze mogą być dowolnego typu                       |
| Elastyczność          | Tylko `true/false` on/off             | Dowolne wartości                                     |
**Dlaczego bitmapa jest bardziej efektywna?**
1. *Minimalne zużycie pamięci:* W bitmapie jeden bit przechowuje jeden stan `true lub false`. W mapie każdy klucz `Integer` i wartość `Boolean` zajmują pamięć na pełny obiekt. W Javie klucz `Integer` zajmuje minimum 16 bajtów (zależnie od JVM), a wartość `Boolean` zajmuje 4-16 bajtów.
2. *Brak narzutu obiektowego:* Bitmapa przechowuje dane w liczbach (int, long) lub tablicach, bez dodatkowego narzutu (takiego jak w mapach: wskaźniki na węzły, hashCode itp.).
3. *Szybsze operacje:* W bitmapie każda operacja `set, get, clear` to błyskawiczna operacja bitowa. W mapie trzeba przeszukiwać strukturę danych (np. HashMap lub TreeMap) co jest wolniejsze.