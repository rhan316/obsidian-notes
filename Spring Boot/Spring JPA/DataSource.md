*DataSource* to fundament pracy z bazą danych w Javie i Springu. Dosłownie fundament.
Bez niego nic nie ruszy - żaden JDBC, JPA, Hibernate, transakcja... nic.

### Co to w ogóle jest?

**`DataSource`** to interfejs, który reprezentuje *źródło połączeń* do bazy danych.
**Tak, interfejs - nie implementacja**. Implementacja zapewnia:
- serwer aplikacji
- biblioteka connection poola (HikariCP, Apache DBCP...)
- Spring Boot (auto-konfiguracja)

Spring traktuje `DataSource` jako bean, który potem wstrzykuje do:
- `JdbcTemplate`
- enitity managerów (JPA)
- mechanizmu transakcji
I tak, dobrze rozumiesz - to jest jak krwiobieg aplikacji. Nie masz DataSource -> aplikacja dostaje zawału.

### Dlaczego jest taki ważny?

Bo trzyma połączenia do bazy. A połączenia są kosztowne.
W profesjonalnych aplikacjach **każde połączenie musi być z puli**, inaczej widzimy OutOfMemory i płacz.

Spring Boot 3 domyślnie używa **HikariCP**, bo jest szybki i stabilny.
W Spring Docs często podkreślają jego rolę w warstwie "transactional data and persistence".

### Gdzie to się ustawia?

Najczęściej w `application.properties`:
```ini
spring.datasource.url=jdbc:postgresql://localhost:5432/app
spring.datasource.username=user
spring.datasource.password=secret
spring.datasource.driver-class-name=org.postgresql.Driver
```
I koniec - Spring Boot sam złoży DataSource.
Można ręcznie przez @Bean ale to rzadkie przypadki.

`DataSource` otwiera połączenia, trzyma je w puli, oddaje do wykorzystania, zamyka tylko wtedy, kiedy pula to uzna i pilnuje validity i timeouty.

### Najważniejsze rzeczy, które musisz zapamiętać:
- DataSource = źródło połączeń
- Spring Boot automatycznie konfiguruje HikariCP
- DataSource jest wymagany dla JPA, JDBC, transakcji
- Trafia jako bean do wszystkiego, co robi z bazą
- Nie twórz połączenia ręcznie. Serio. Chyba że chcesz coś rozpierdolić.