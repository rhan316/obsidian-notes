### Dlaczego HikariCP jest domyślny?

HikariCP jest szybki - jeden z najszybszych pooli na JVM, lekki - minimalny narzut pamięci i CPU, stabilny - mniej magii, więcej performance.
I to nie są puste slogany. Spring Boot go wybrał właśnie dlatego, a nie dla koloru logo.

### Co robi pool połączeń?
*Jezu Chryste, jeśli tego nie powiesz na rozmowie, to już masz minusy.*

`Pool`:
- trzyma otwarte połączenia do bazy,
- wydaje je w razie potrzeby,
- nie otwiera ich od nowa za każdym razem,
- kontroluje timeout-y, health check-i itd.
Dlatego aplikacji nie dławi się.

### Najważniejsze parametry (które padną na rozmowie kwalifikacyjnej)

`maximumPoolSize` - maksymalna liczba połączeń
`minimumIdle` - ile połączeń ma zawsze czekać
`connectionTimeout` - ile czekasz, zanim rzuci wyjątek
`idleTimeout` - kiedy wywali bezczynne połączenia
`maxLifetime` - "czas życia" połączenia, potem zawsze tworzone nowe.

*Dlaczego nie robić maximumPoolSize = 10000*?
Bo połączenia do bazy są ciężkie. Dajesz tyle, ile serwer bazy jest w stanie obsłużyć.

*Jak sprawdzić, czy problem leży w Hikari, czy w bazie?*
- zajrzeć do metryki poola (ile połączeń jest w użyciu / ile czeka)
- zobaczyć, czy `connectionTimeout` wywala - wtedy pool nie dostaje połączeń - problem po stronie DB
- sprawdzić logi slow queries.