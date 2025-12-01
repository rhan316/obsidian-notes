
### Czym jest Spliterator?
Spliterator to interfejs wprowadzony w JDK 8, znajdujący się w pakiecie `java.util`.
Został stworzony jako nowoczesna alternatywa dla `Iterator`, szczególnie pod kątem:
- równoległego przetwarzania (Streams)
- efektywnego dzielenia danych
- lepszej charakterystyki źródła danych
Spliterator to fundament działania Stream API, zwłaszcza parallel streams.

Można go stosować do: kolekcji, tablic, generatorów i własnych struktur danych.

### Tworzenie Spliteratora
Każda klasa implementująca `Collection` posiada metodę:
```java
Spliterator<T> spliterator();
```
Możesz też tworzyć spliteratory ręcznie, np. poprzez `Spliterators.spliterator(...), Arrays.spliterator(...)`

### Kluczowe metody Spliteratora

`boolean tryAdvance(Consumer<? super T> action)`
- przetwarza dokładnie jeden element
- zwraca: `true->` jeśli jest kolejny element, `false->` jeśli elementów brak.
Np.
```java
spliterator.tryAdvance(System.out::println);
```
To odpowiednik `Iterator.next()`, ale z callbackiem.

`void forEachRemaining(Consumer<? super T> action)`
Przetwarza wszystkie pozostałe elementy.
Jest szybsze od manualnego `while(tryAdvance)`
