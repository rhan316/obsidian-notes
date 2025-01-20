**Co to jest współbieżność?**

Współbieżność to możliwość wykonywania wielu zadań w tym samym czasie. W programowaniu oznacza to, że możesz podzielić swój kod na różne wątki (threads), które działają jednocześnie.

**Wątki VS procesy**

Proces to coś większego - jak cała restauracja. Wątek to pojedynczy kucharz w tej restauracji. Wątki współdzielą ten sam obszar pamięci, więc mogą pracować nad tymi samymi danymi (np. współdzielić jedno danie, które mają przygotować).

**Problemy współbieżności**

1. *Blokady (deadlocks)* - Dwóch kucharzy może próbować kroić tę samą marchewkę w tym samym czasie.
2. *Warunki wyścigu (race conditions)* - Kto pierwszy skończy zadanie? Jeśli jeden kucharz zacznie podawać danie, zanim drugi doda przyprawy, danie będzie nieskończone.
3. i inne...

W Javie istnieją dwa podstawowe sposoby na tworzenie wątków: za pomocą interfejsu Runnable oraz rozszerzenia klasy Thread.


| Cecha               | Runnable                                                           | Thread                                                            |
| ------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------- |
| Dziedziczenie       | Klasa może dziedziczyć z innej klasy (większa elastyczność)        | Klasa nie może dziedziczyć z innej klasy (bo dziedziczy z Thread) |
| Modularność         | Logika zadania jest oddzielona od klasy wątku                      | Logika zadania i wątek są w jednej klasie                         |
| Zastosowanie        | Lepsze w skomplikowanych projektach, gdzie ważna jest elastyczność | Lepsze dla prostych zastosowań                                    |
| Tworzenie instancji | Wymaga stworzenia obiektu Runnable i przekazania go do Thread      | Tworzysz bezpośrednio obiekt klasy dziedziczącej Thread           |
*Kiedy wybrać Runnable, a kiedy Thread?*
1. *Runnable* - Używaj, gdy Twoja klasa musi dziedziczyć z innej klasy (np. dla elastyczności i większej modularności)
2. *Thread* - Używaj, gdy chcesz szybko zaimplementować wątek i nie potrzebujesz dziedziczenia

