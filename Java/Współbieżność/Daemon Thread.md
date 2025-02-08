To specjalny rodzaj wątku, który działa w tle i wykonuje zadanie pomocnicze lub mniej istotne. Jest używany głównie do wspierania głównych wątków aplikacji, a jego kluczowa cecha to, **brak blokady zakończenia programu** - JVM zakończy działanie, nawet jeśli wątek daemon ciągle działa.

**Czy jest daemon thread?**
Daemon thread to wątek o niższym priorytecie, który działa w tle i wykonuje zadania, które nie są kluczowe dla aplikacji. Przykładem daemon są:
1. Garbage Collector (GC).
2. Wątki monitorujące (np. obserwujące zmiany w systemie plików).
3. Wątki zarządzające cache.

**Główne cechy daemon thread:**
1. ~={cyan}*Nie blokuje zamknięcia JVM*=~ - Jeśli wszystkie wątki użytkownika (tzw. "non-daemon threads") zakończą swoje działanie, JVM automatycznie zakończy pracę, nawet jeśli wątki daemon nadal działają.
2. ~={cyan} *Tworzenie wątków daemon*=~ - Wątki daemon można tworzyć, ustawiając ich właściwość `setDaemon(true)` przed ich uruchomieniem `start()`;
3. ~={cyan}*Domyślny charakter potomków*=~ - Jeśli wątek daemon utworzy nowy wątek, nowy wątek automatycznie staje się daemonem.
4. ~={cyan}*Nie jest 'zaufany'*=~ - Wątki daemon mogą zostać niespodziewanie przerwane w trakcie działania, jeśli JVM zakończy swoją pracę. Nie należy używać ich do działań wymagających niezawodności, takich jak zapis danych.

| Cecha         | Wątek Daemon                                      | Wątek Non-Daemon                                      |
| ------------- | ------------------------------------------------- | ----------------------------------------------------- |
| Priorytet     | Niski                                             | Zwykle wyższy                                         |
| Zamykanie JVM | JVM kończy pracę, gdy działają tylko wątki daemon | JVM czeka na zakończenie wszystkich wątków non-daemon |
| Przykłady     | Garbage Collector, monitorowanie zdarzeń          | Główne wątki aplikacji, obsługa użytkownika           |
| Zastosowanie  | Zadania pomocnicze                                | Kluczowe operacje                                     |

