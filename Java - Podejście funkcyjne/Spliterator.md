
Interfejs wprowadzony w Javie 8, który służy do przechodzenia (iteracji) przez elementy danych w kolekcjach, ale jednocześnie oferuje mechanizmy do podziału zbioru elementów na mniejsze podzbiory. Można go znaleźć w pakiecie java.util

**Metoda spliterator()**

```
Wszystkie klasy implementujące interfejs Collection posiadają metodę spliterator(). Metoda ta zwraca instancję Spliterator, która może być wykorzystana do równoległego przetwarzania elementów.

Spliterator<T> spliterator()

Podstawowe funkcje Spliteratora:

1. tryAdvance(Consumer<? super T> action) - przechodzi przez elementy wykonując przekazaną operację dla kożdego elementu, dopóki są one dostępne.
	spliterator.tryAdvance();
2. forEachRemaining(Consumer<? super T> action) - przetwarza wszyskie pozostałe elementy, wywołując podaną akcję dla każdego z nich
	spliterator.forEachRemaining();
3. trySplit() - próbuje podzielić elementy na mniejsze podzbiory, co umożliwia równoległe przetwarzanie danych => trySplit() dzieli spliterator na dwa - orginalny Spliterator oraz nowy, który przechowuje część danych. Ma to duże zastosowanie przy równoległym przetwarzaniu, ponieważ umożliwia przetwarzanie danych w różnych wątkach
```

Właściwości Spliteratora => Cechy te są określane metodą characteristics(), która zwraca wartość bitową reprezentującą zestaw cech spliteratora

| Cechy      |                                                                           |
| ---------- | ------------------------------------------------------------------------- |
| ORDERED    | Elementy są przetwarzane w określonej kolejności (np. lista)              |
| DISTINCT   | Wszystkie elementy są unikalne                                            |
| SORTED     | Elementy są posortowane                                                   |
| SIZED      | Spliterator zna dokładną liczbę elementów, które zostały do przetworzenia |
| CONCURRENT | Kolekcja może być modyfikowana przez inne wątki podczas przetwarzania     |
