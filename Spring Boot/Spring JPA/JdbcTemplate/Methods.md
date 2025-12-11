
### `.execute(String sql)`

Służy przede wszystkim do komend SQL, które zmieniają strukturę bazy, a nie dane.
Powtarzam - strukturę bazy, nie dane.
Takie komendy nazywamy `DDL` (Data Definition Language).
Np. 
`CREATE TABLE ...`  `ALTER TABLE ...` `DROP TABLE ...` `CREATE INDEX ...`

---

### `.update(...)`

Służy do aktualizacji lub umieszczania danych do bazy. Istnieje sporo wariantów do zadań w batch.
`update()` jest przeciążone. --> `int update(String sql, [...])`
Zwraca ilość wierszy zmienionych przez tą metodę.

### `<T> T queryForObject(String sql, Class<T> reqType [..]`
Zwraca tylko jeden element.
```java
int size = jdbcTemplate
	.queryForObject("SELECT COUNT(*) FROM Profile", Integer.class);
```

### `Placeholder ?`

**Jak działa placeholder `?`**
1. Silnik JDBC przygotowuje zapytanie jako plan.
2. Parametry przekazywane po `?` są bindowane.
3. Wartość jest traktowana jak dane, nie instrukcje SQL.
4. Koniec zabawy z SQL Injection.

```pgsql
String sql = "SELECT * FROM users WHERE age > ?";
jdbcTemplate.query(sql, new Object[]{30}, rowMapper);
```
Hej, baza, wykonaj zapytanie, a tutaj masz parametr na miejsce `?`

