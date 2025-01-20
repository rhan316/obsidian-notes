
| Cechy                  | Wielowątkowość                       | Asynchroniczność                                | Współbieżność                                              |
| ---------------------- | ------------------------------------ | ----------------------------------------------- | ---------------------------------------------------------- |
| Definicja              | Równoległe wykonywanie wątków        | Wykonywanie zadań bez blokowania głównego wątku | Obsługa wielu zadań jednocześnie                           |
| Wymaga wielowątkowości | Tak                                  | Nie                                             | Nie zawsze                                                 |
| Przykład               | Kilka wątków obsługuje różne zadania | Jedno zadanie jest uruchamiane w tle            | System obsługuje wiele zadań, przełączając się między nimi |
| Analogia               | Kilku pracowników w fabryce          | Zamawianie pizzy                                | Jedna osoba obsługująca wielu klientów                     |
***Wielowątkowość (Multithreading)***
To technika, w której wiele wątków (ang. threads) działa jednocześnie w ramach tego samego procesu.
Wątek to najmniejsza jednostka przetwarzania, która może być wykonywana przez procesor.

*Jak to działa?*
Wątek działa niezależnie, ale współdzieli pamięć i zasoby z innymi wątkami w tym samym procesie.
Można używać wielowątkowości, aby równolegle wykonywać różne zadania.

*Analogia*
Fabryka z pracownikami.
Każdy pracownik (wątek) zajmuje się swoją częścią zadania (np. montuje jeden element produktu).
Wszyscy współdzielą zasoby fabryki (np. narzędzia, maszyny).

*Kluczowe cech*y
**Równoległość** Jeśli masz procesor wielordzeniowy, różne wątki mogą być wykonywane równocześnie (równolegle).
**Współdzielenie zasobów** Wątki współdzielą pamięć, co może prowadzić do problemów, takich jak konflikty w dostępie do danych.


***Asynchroniczność (Asynchrony)***

*Co to jest?*
**Asynchroniczność** oznacza wykonywanie zadania w tle bez blokowania głównego wątku. Gdy zadanie kończy się, system powiadamia o tym wyniku.

*Jak to działa?*
Asynchroniczne operacje niekoniecznie muszą być wielowątkowe. Mogą być obsługiwane przez jeden wątek, który realizuje zadania jedno po drugim.

*Analogia*
Zamawiasz pizzę:
Składasz zamówienie (asynchronicznie) i wracasz do swoich zajęć.
Gdy pizza jest gotowa, dostajesz powiadomienie lub pizzę dostarczają pod drzwi.

*Kluczowe cechy*
**Nie blokuje**, główny program nie czeka na zakończenie operacji - może kontynuować inne zadania.
**Zwykle jednokierunkowe** Wątek wykonuje zadania i informuje o zakończeniu, ale nie wymaga bezpośredniego współdziałania.


***Współbieżność (Concurrency)***

**Co to jest?**
Współbieżność oznacza zdolność systemu do obsługi wielu zadań w tym samym czasie.
Może to być realizowane za pomocą wielowątkowości lub asynchroniczności, ale nie zawsze oznacza równoległe wykonywanie zadań.

**Jak działa?**
Program współbieżny przełącza się między różnymi zadaniami, tak aby wyglądało, że są wykonywane jednomyślnie, nawet jeśli faktycznie są wykonywane sekwencyjnie na jednym wątku.

**Analogia**
Jedna osoba (procesor) obsługująca wiele klientów w sklepie.
Osoba obsługuje jednego klienta, ale jeśli klient czeka na coś (np. szuka pieniędzy), obsługująca osoba przechodzi do kolejnego klienta.

**Kluczowe cechy**
Nie zawsze równoległość - Może wyglądać, jakby zdania były wykonywane jednocześnie, ale w rzeczywistości procesor przełącza się między nimi.
Podział zasobów - System dzieli czas i zasoby między wiele zadań.
