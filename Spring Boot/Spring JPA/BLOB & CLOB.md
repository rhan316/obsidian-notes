
### BLOB -> Binary Large Object

Przechowujesz w postaci binarnej zdjęcia, PDF-y, pliki i inne dane niestandardowe.

### CLOB -> Character Large Object

Przechowujesz bardzo dużo teksty: JSON-y, XML-e, długie opisy, dokumenty tekstowe.


| DB         | BLOB       | CLOB       |
| ---------- | ---------- | ---------- |
| PostgreSQL | `bytea`    | `text`     |
| Oracle     | `BLOB`     | `CLOB`     |
| MySQL      | `LONGBLOB` | `LONGTEXT` |
### BLOB CLOB w JPA

Tu zaczyna się magiczny cyrk ORM-owy:
Używasz adnotacji:
**BLOB**
```java
@Lob
private byte[] data;
```
**CLOB**
```java
@Lob
private String description;
```
**Hibernate sam rozpoznaje, czy ma użyć BLOB/CLOB**.

Ale uwaga:
przy BLOB-ach -> JPA lubi robić lazy loading (czasem wkurzające)
przy dużych danych -> nie przesadzaj, używaj streamów, nie recordów z 50MB pola

### Ważne praktyki

**Nie wkładaj ogromnych plików do DB**
Baza to nie dysk.
Do plików -> S3, MiniIO, lokalny storage.
Do DB -> tylko metadane.

**BLOB-y i CLOB-y mogą obciążyć transakcje**
To duże dane, mogą blokować.

**Używaj streamów jeśli to możliwe**
Spring umożliwia: `ps.setBinaryStream(2, inputStream);`

**Uważaj na JPA + BLOB**
Możesz przypadkiem pobierać cały plik przy każdym SELECT.
To koszmar.

---
### JdbcTemplate

INSERT BLOB
```java
String sql = "INSERT INTO files (name, data) VALUES (?, ?)";

jdbcTemplate.update(sql, ps -> {
	ps.setString(1, "plik.pdf");
	ps.setBytes(2, fileBytes);
});
```
Odczyt
```java
byte[] data = jdbcTemplate.queryForObject(
	"SELECT data FROM files WHERE id = ?",
	(rs, m) -> rs.getBytes("data"),
	id
);
```

### JdbcClient

INSERT BLOB
```java
client.sql("INSERT INTO files(name, data) VALUES(:name, :data)")
	.param("name", "plik.pdf")
	.param("data", fileBytes)
	.update();
```
Odczyt
```java
Optional<byte[]> data = 
	client.sql("SELECT data FROM files WHERE id = :id")
		.param("id", id)
		.query(byte[].class)
		.optional();
```