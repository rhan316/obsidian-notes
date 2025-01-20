
`CompletableFuture` to narzędzie do prostego zarządzania współbieżnością i asynchronicznością w Javie.

Pozwala na wykonywanie operacji w tle, łączenie ich wyników i obsługę wyjątków w elegancki sposób.

Dzięki metodom takimi jak `thenApply` i `exceptionally` łatwo budować przepływ danych i zarządzać błędami.

**Czym jest `CompletableFuture`?**
`CompletableFuture` to klasa w Javie, która służy do obsługi operacji asynchronicznych i współbieżnych. Jest częścią pakietu `java.util.concurrent`, wprowadzonego w JDK 8. Dzięki niej możemy wykonywać zadania w tle, a wynik obsługiwać, gdy będzie gotowy, bez blokowania głównego wątku.

**Podstawowe cechy `CompletableFuture`**
1. *Obsługa asynchronicznych zadań* - Wykonywanie kodu w tle.
2. *Łańcuchowe przetwarzanie* - Możliwość łączenia operacji (np. po zakończeniu jednej od razu zaczyna się kolejna).
3. *Reagowanie na wynik*: Obsługa zarówno sukcesu, jak i błędów.
4. *Integracja z `ExecutorService`*: Możliwość wykonywania zadań w niestandardowych wątkach.

***Podstawowe metody `CompletableFuture`***

| Metoda                | Opis                                                                      |
| --------------------- | ------------------------------------------------------------------------- |
| `runAsync()`          | Uruchamia zadanie asynchroniczne bez zwracania wyniku                     |
| `supplyAsync()`       | Uruchamia zadanie asynchroniczne i zwraca wynik                           |
| `thenApply()`         | Przetwarza wynik asynchronicznie (po zakończeniu poprzedniego zadania)    |
| `thenAccept()`        | Przyjmuje wynik, ale nic nie zwraca (konsument wyniku)                    |
| `exceptionally`       | Obsługuje wyjątki, które wystąpiły podczas asynchronicznego przetwarzania |
| `join()`              | Zwraca wynik operacji, czekając na jej zakończenie                        |
| `allOf()` / `anyOf()` | Obsługuje wiele `CompletableFuture` (wszystkie lub dowolny z nich)        |

