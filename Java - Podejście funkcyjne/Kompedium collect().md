
### Co to w ogóle jest `collect()`?

`collect()` to najpotężniejsza operacja końcowa w Stream API.
Reduce? Filter? Map? To maluchy.

`collect()` to:
- budowanie kolekcji,
- tworzenie własnych struktur,
- grupowanie,
- łączenie,
- agregowanie,
- operacje na mutowalnych kontenerach,
- równoległa redukcja na mutowalnych strukturach.

To fabryk wyników.
Koniec gadania.

## 3 wersje - i każda jest inna

### `collect(Collector<T, A, R> collector`

To jest ta wersja, której prawie zawsze używasz:
```java
List<String> names = stream.collect(Collectors.toList());
```
`Collector` ma 4 elementy:
- *supplier* -> tworzy pusty wynik
- *accumulator* -> dodaje element strumienia do wyniku
- *combiner* -> łączy dwa częściowe wyniki (parallel stream!)
- *finisher* -> przetwarza wynik końcowy (czasem pomijany)
To fundament.

### `collect(Supplier, BiConsumer, BiConsumer)`

Czyli kolektor "na żywca", DIY, bez Collectors:
```java
List<String> list = stream.collect(
	ArrayList::new, // supplier
	List::add, // accumulator
	List::addAll // combiner
)
```