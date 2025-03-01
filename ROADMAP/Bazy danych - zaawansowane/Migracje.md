**Migracje SQL** to proces modyfikowania struktury bazy danych w kontrolowany i powtarzalny sposób. Oznacza to, że zamiast ręcznie edytować tabelę za pomocą `ALTER TABLE`, stosujemy zorganizowane skrypty migracyjne, które umożliwiają:
- Dodawanie/usuwanie tabel i kolumn.
- Zmianę typów danych.
- Aktualizację relacji i indeksów.
- Wypełnianie bazy danych początkowymi (seed).

*Analogia: Migracje to wersjonowanie bazy danych*
Wyobraź sobie grę komputerową. Każda aktualizacja gry (np. v1.1 -> v.1.2) wprowadza zmiany, np. nową mapę czy poprawki błędów.
Podobnie migrację w SQL umożliwiają stopniowe aktualizowanie struktury bazy danych bez utraty istniejących danych.

Spring Boot wspiera dwa główne podejścia do migracji SQL:
1. Hibernate auto-ddl (Automatyczna migracja)
2. Liquibase / Flyway (Migracje wersjonowane)

### Automatyczne migracje w Hibernate `spring.jpa.hibernate.ddl-auto`

*Spring Boot może samodzielnie aktualizować schemat bazy, ale nie wersjonuje zmian!!!*

Spring Boot odczytuje encję JPA `@Entity` i automatycznie dostosowuje tabelę do modelu.
```properties
spring.jpa.hibernate.ddl-auto=update
```
Działanie:
Jeśli dodasz nową kolumnę w klasie `User`, Spring automatycznie doda ją do tabeli.
Ale nie zapisuje historii zmian, więc nie można cofnąć migracji!

```java
@Enitiy
public class User {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private long id;

	@Column(nullable = false)
	private String username;

	@Column(unique = true) // Nowa kolumna
	private String email;
}
```
Efekt: Spring Boot automatycznie doda kolumnę `email` do tabeli `User`.
Problem: Jeśli usuniesz kolumnę `email`, Hibernate nie usunie jej z bazy danych! Dlatego do profesjonalnych migracji używamy *Flyway lub Liquibase*.


### Migracje SQL w Spring Boot z Flyway
*Flyway to narzędzie do wersjonowania migracji SQL*

**Jak to działa?**
Tworzysz pliki SQL ze zmianami w katalogu `src/main/resources/db/migration`
Flyway wykonuje je automatycznie przy starcie aplikacji
Każda migracja ma numer wersji `V1_init.sql`, `V2_add_email.sql`.

`... Instalacja i konfiguracja ...`

**Pierwsza migracja: Tworzenie tabeli `V1_create_user.sql`**
```sql
CREATE TABLE users (
	id BIGINT AUTO_INCREMENT PRIAMRY KEY,
	username VARCHAR(255) NOT NULL,
	email VARCHAR(255) UNIQUE
);
```

**Druga migracja: Dodanie nowej kolumny `V2_add_status.sql`**
```sql
ALTER TABLE users ADD COLUMN status VARCHAR(20) DEFAULT 'ACTIVE';
```

**Cofanie migracji (rollback)**
Flyway nie wspiera `ROLLBACK`, ale można dodać migrację `UNDO` `V3_remove_status.sql`
```sql
ALTER TABLE users DROP COLUMN status;
```
*Efekt:*
- Historia migracji jest zapisywana w tabeli `flyway_schema_history`.
- Można łatwo przywracać poprzednie wersje bazy.

### Migracje SQL w Spring Boot z Liquibase
*Liquibase działa jak Flyway, ale zamiast czystego SQL używa plików XML, YAML lub JSON do opisania zmian*.

`... Instalacja i konfiguracja ...`

**Główny plik `db.changelog-master.json` wskazuje na wszystkie zmiany migracyjne**
```json
{
	"databaseChangeLog": [
		{ "include": {"file": "db/changelog/changesets/001_create_users.json"} },
		{ "include": { "file": "db/changelog/changesets/002_add_email.json" } }
	]
}
```