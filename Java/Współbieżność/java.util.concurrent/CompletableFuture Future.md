`Future` reprezentuje wynik obliczeń asynchronicznych, które mogą się jeszcze nie zakończyć.
Główne ograniczenia:
- ~={red}Blokujący dostęp=~ - Metoda `get()` blokuje wątek, aż wynik będzie dostępny.
- ~={cyan}Brak kontroli=~ - Nie można anulować lub modyfikować zadania po jego uruchomieniu.
- ~={green}Brak łańcuchowania=~ - `Future` nie wspiera wykonywania dalszych operacji po zakończeniu zadania.

`CompletableFuture` to rozszerzenie `Future`, które wspiera programowanie reaktywne.
Główne zalety:
- ~={8}Nieblokujące operacje=~: Metody takie jak `thenApply()`, `thenAccept()` i `thenRun()` pozwalają na wykonanie kodu po zakończeniu zadania bez blokowania wątku.
- ~={magenta}Obsługa wyjątków=~: Możesz obsłużyć błędy za pomocą `exceptionally()` lub `handle()`.
- ~={red}Łańcuchowanie=~: Umożliwia tworzenie skomplikowanych przepływów asynchronicznych dzięki metodom takim jak `thenCompose()` i `thenCombine()`.
- ~={blue} Kompozycja=~: Można łatwo łączyć wiele zastosować asynchronicznych.


| Cecha            | Future               | CompletableFuture      |
| ---------------- | -------------------- | ---------------------- |
| Blokowanie       | Tak (metoda `get()`) | Nie (reaktywne metody) |
| Łańuchowanie     | Nie                  | Tak                    |
| Obsługa wyjątków | Nie                  | Tak                    |
| Kompozycja       | Ograniczona          | Rozbudowana            |
