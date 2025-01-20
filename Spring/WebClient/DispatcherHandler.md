`DispatcherHandler` jest kluczowym komponentem w `Spring WebFlux`, odpowiedzialnym za obsługę przechodzących żądań HTTP i ich przekierowywanie do odpowiednich komponentów, takich jak kontrolery i filtry. W kontekście `WebClient`, `DispatcherHandler` odgrywa rolę w obsłudze asynchronicznych i reaktywnych żądań, kiedy jest używany na serwerze (np. w aplikacji działającej w ramach `Spring WebFlux`).

***Jak działa `DispatcherHandler`?***
~={red}*Centralny punkt obsługi żądań*=~ - pełni funkcję obsługi każdego żądania HTTP i zarządza ich przepływem.
~={green}*Reaktywny przepływ żądań* =~- Nie działa w sposób blokujący, dzięki czemu jest w stanie obsługiwać wiele żądań równocześnie. Wykorzystuje *Reactive Streams* i architekturę opartą na *Project Reactor*, aby zapewnić pełną asynchroniczność.
~={yellow}*Delegacja do handlerów*=~ - `DispatcherHandler` deleguje przetwarzanie żądań do odpowiednich **handlerMapping, HandlerAdapter, czy HandlerResultHandler** od konfiguracji aplikacji.

