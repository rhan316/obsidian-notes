To zrównoważone drzewa wyszukiwania zaprojektowane specjalnie do optymalizacji operacji na dużych zbiorach danych, szczególnie w kontekście baz danych i systemów plików. Są one efektywne pod względem liczby operacji dyskowych, ponieważ minimalizują liczbę odczytów i zapisów z pamięci masowej.

#### Czym jest B-drzewo?

B-drzewo to samobalansujące drzewo wyszukiwania, które pozwala na więcej niż dwóch potomków na węzeł (nie jest to drzewo binarne). Dzięki temu może przechowywać wiele kluczy w jednym węźle, co zmniejsza liczbę poziomów w drzewie, a tym samym przyspiesza operację wyszukiwania.

**Podstawowe właściwości B-drzewa (dla rzędu t-tzw. "stopnia" drzewa):**

Każdy węzeł może przechowywać od `t-1` do `2t-1` kluczy.
(Minimum `t-1`, max `2t-1` ogranicza rozrost drzewa).

Każdy węzeł może mieć od `t` do `2t` dzieci.
Dzięki temu drzewa ma mniejszą wysokość, co poprawia wydajność.

Wszystkie liście są na tym samym poziomie.
To zapewnia zrównoważenie drzewa - żadna gałąź nie jest dłuższa od innej.

Gdy węzeł jest przepełniony `2t-1` kluczy, dzielimy go na dwa mniejsze i promujemy środkowy klucz rodzica.
To utrzymuje rozmiar drzewa w granicach `O(log n)`

----

#### Jak działa wyszukiwanie w B-drzewie?
Szukamy w katalogu w bibliotece - zamiast przeszukiwać wszystkie półki, patrzymy na główny indeks, który kieruje nas do właściwej sekcji.

**Algorytm wyszukiwania**
1. Porównujemy szukany klucz z wartościami w węźle.
2. Jeśli klucz znajduje się węźle - sukces.
3. Jeśli nie, przechodzimy do odpowiedniego dziecka (wybierając zakres, w którym może znajdować się klucz).
4. Powtarzamy aż do znalezienia klucza lub dotarcia do liścia.

Z powodu mniejszej wysokości drzewa `O(log_t n)` wyszukiwanie jest szybsze niż w klasycznym BST `O(log_2 n)`, ponieważ przeszukujemy mniej poziomów.