
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


### Cechy Spliteratora (characteristics)

Każdy Spliterator może mieć zestaw flag opisujących dane źródło. Są ważne, bo Stream API używa ich do optymalizacji - zwłaszcza w trybie równoległym (parallel streams).

Najważniejsze:

| Nazwa                      | Opis                                                                              |
| -------------------------- | --------------------------------------------------------------------------------- |
| **SIZED**                  | znam liczbę elementów                                                             |
| **SUBSIZED**               | każdy wynik `trySplit()` też zna swój rozmiar                                     |
| **SORTED**                 | elementy są posortowane                                                           |
| **DISTINCT**               | brak duplikatów                                                                   |
| **NONNULL**                | nie ma wartości null (i bardzo dobrze)                                            |
| **IMMUTABLE / CONCURRENT** | źródło nie zmienia się w trakcie iteracji albo jest odporne na zmiany współbieżne |
To nie są ozdoby - Stream korzysta z nich, żeby dobrać strategię dzielenia pracy. Bez nich w parallel streamch masz gówno, nie wydajność.

#### `trySplit()` - serce równoległego streamowania
`Spliterator<T> trySplit()`
- dzieli dane na dwa spliteratory
- jeśli nie da się podzielić (np. dane są z natury sekwencyjne), zwraca `null`
- to mechanizm `fork-join` w czystej postaci
Im lepiej zaimplementowane dzielenie, tym bardziej opłaca się parallel stream.

`estimateSize()` -> podaje przybliżoną liczbę elementów (lub dokładną, jeśli jest znana)
`getExactSizeIfKnown()` -> zwraca dokładany rozmiar lub `-1`, jeśli nie wiadomo


| **Iterator**          | **Spliterator**                                 |
| --------------------- | ----------------------------------------------- |
| Jednowątkowy          | Zaprojektowany pod wielowątkowość               |
| `next()`, `hasNext()` | `tryAdvance()`, `forEachRemaining()`            |
| Brak dzielenia        | `trySplit()` umożliwia równoległe przetwarzanie |
| Stary jak cholera     | Fudament Stream API                             |
