**NEW** - nowy
**RUNNABLE** - wykonywalny
**BLOCKED** - zablokowany
**WAITING** - oczekujący
**TIME WAITING** - oczekujący określoną ilość czasu
**TERMINATED** - zakończony

~={green}**NEW (Nowy)**=~
Wątek został stworzony, ale jeszcze nie rozpoczął pracy.
- Wątek jest w stanie *NEW* zaraz po utworzeniu obiektu wątku, ale przed wywołaniem metody `start()`.
- To jak nowo zatrudniony pracownik, który właśnie podpisał umowę o pracę, ale jeszcze nie pojawił się w fabryce.
- Wywołanie `start()` przenosi wątek do stanu *RUNNABLE*.
`Thread t = new Thread(); // Stan NEW`

~={green}**RUNNABLE (Gotowy do działania)**=~
Wątek jest gotowy do wykonania i czeka, aż procesor go obsłuży.
- Wątek trafia w stan *RUNNABLE* po wywołaniu `start()`.
- Pracownik czeka na szkolenie, jest na linii produkcyjnej i czeka na swoją kolej, aby faktycznie rozpocząć pracę.
- Wątek może przejść do stanu *RUNNING* (kiedy procesor zacznie go wykonywać) lub *WAITING/BLOCKED*, jeśli musi czekać.
`t.start(); // Przejście do RUNNABLE`

~={green}**RUNNING (Wykonywany)**=~
Wątek faktycznie jest wykonywany przez procesor.
- Harmonogram procesora decyduje, który wątek w stanie *RUNNABLE* przejdzie do stanu *RUNNING*.
- Pracownik faktycznie pracuje przy swoim stanowisku.
- Wątek może przejść do *BLOCKED/WAITING*, jeśli napotka przeszkodę, lub *TERMINATED*, jeśli zakończy pracę.
*UWAGA!* Nie ma bezpośredniego sposobu, by sprawdzić, czy wątek jest w stanie RUNNING - ten stan jest krótkotrwały.

~={green}**BLOCKED/WAITING (Zablokowany/Oczekujący)**=~
Wątek tymczasowo czeka na pewne zasoby lub zdarzenia.
- *WAITING* - Wywołanie metod takich jak `wait()` lub `join()` powoduje, że wątek czeka na sygnał.
- *BLOCKED* - Wątek czeka na dostęp do sekcji krytycznej (np. przy współdzieleniu zasobów).
- Pracownik stoi przy stanowisku, ale nie może pracować, bo np. brakuje narzędzi lub czeka na instrukcje od menedżera.
- Wątek przejdzie z powrotem do *RUNNABLE*, gdy zasoby staną się dostępne.
`synchronized (this) { wait(); } // Wątek w stanie WAITING`

~={green}**TERMINATED (Zakończony)**=~
Wątek zakończył swoją pracę i nie może już być ponownie uruchomiony.
- Stan *TERMINATED* występuje po zakończeniu metody `run()` lub po zamknięciu wątku.
- Pracownik ukończył swoje zadanie i opuścił fabrykę.
- Wątek w stanie *TERMINATED* nie może wrócić do życia.
`t.join(); // Wątek kończy pracę.`


**Diagram stanów wątku**
```
NEW --> RUNNABLE --> RUNNING --> TERMINATED
        |               |
        v               v
    WAITING/BLOCKED <----

```
