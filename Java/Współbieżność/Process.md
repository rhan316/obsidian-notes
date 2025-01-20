**Czym są wątki w procesie?**
Każdy proces składa się z *wątków (ang. threads)*. Wątek to najmniejsza jednostka wykonywania w obrębie procesu. Proces może mieć jeden wątek (wątek główny) lub wiele wątków, które działają równolegle i współdzielą zasoby procesu, takie jak pamięć i dane. 

**Procesy w Javie**
W Javie procesy zarządzane są za pomocą klasy `Process` z pakietu `java.lang`. Klasa ta reprezentuje proces, który może być uruchomiony przez aplikację Java przy użyciu klasy `ProcessBuilder` lub metod z klasy `Runtime`.

**Różnice między procesami a wątkami**

| Cecha            | Proces                        | Wątek                                   |
| ---------------- | ----------------------------- | --------------------------------------- |
| Izolacja         | Procesy są izolowane          | Wątki współdzielą pamięć                |
| Zasoby           | Każdy proces ma własne zasoby | Wątki dzielą zasoby procesu             |
| Przykład w Javie | `Process`, `ProcessBuilder`   | `Thread`, `Runnable`, `ExecutorService` |
**Dlaczego procesy są przydatne?**
Procesy pozwalają na uruchomianie i zarządzanie zewnętrznymi aplikacjami oraz izolowanie programów w celu zwiększenia bezpieczeństwa. Na przykład: Jeśli jeden proces się zawiesi, inne procesy nadal działają. Procesy mogą komunikować się ze sobą.

**Kiedy używać `Process`?**
- Automatyzacja zadań systemowych: Uruchamianie skryptów, poleceń czy zewnętrznych programów.
- Komunikacja z innymi aplikacjami: Wywoływanie innych programów, np. konwerterów plików czy testów.
- Obsługa narzędzi developerskich: Wywoływanie procesów takich jak `mvn`, `gradle` czy `npm`.