Iterator w Javie to interfejs, który pozwala przechodzić po elementach kolekcji w sposób kontrolowany. Interfejs ten jest częścią pakietu java.util i zapewnia metody do iteracji po kolekcji, takie jak:

```
1. boolean hasNext(): Sprawdza, czy są jeszcze elementy do iterowania. Zwraca true, jeśli są.
2. T next(): Zwraca następny element w kolekcji.
3. void remove(): Usuwa ostatni element zwrócony przez next()
```

Różnice między Iterable a Iterator


| Iterable                                                                            | Iterator                                                      |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Interfejs, który reprezentuje kolekcję, którą można przeglądać element po elemencie | Interfejs umożliwiający iterację w kolekcji                   |
| Zawiera metodę iterator(), która zwraca obiekt Iterator                             | Posiada metody hasNext(), next(), remove() i inne(opcjonalne) |
| Używa się go w pętlach for-each                                                     | Daje większą kontrolę nad procesem iteracji niż Iterable      |
