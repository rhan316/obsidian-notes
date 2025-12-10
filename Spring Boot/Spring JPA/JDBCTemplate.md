JdbcTemplate to taka sprytna nakładka na czyste JDBC, która:
- usuwa powtarzalny syf (`try/catch, close(), finally`)
- zarządza połączeniami za ciebie (DataSource)
- daje proste metody do wykonywania SQL
- mapuje wyniki bez bólu istnienia
To nie jest magia. To utility class, która mówi:
"Hej, devie, po co masz pisać 18 linijek boilerplate'u, skoro mogę zrobić to za ciebie?"

### Jak to działa?

JdbcTemplate nie ukrywa SQL'a.
To jest nadal twoje zapytanie tylko mniej kodu, mniej wyjątków, mniej okazji aby coś spierdolić.

Np. w JDBC:
```java
Connection c = dataSource.getConnection();
PreparedStatement ps = c.prepareStatement("SELECT * FROM user WHERE id = ?");
ps.setLong(1, id);
ResultSet rs = ps.executeQuery();
...
rs.close();
ps.close();
c.close();

```

W JdbcTemplate robisz tak:
```java
var user = jdbcTemplate.queryForObject(
	"SELECT * FROM user WHERE id = ?",
	new BeanPropertyRowMapper<>(User.class),
	id
);
```
I tyle!
Zero `finally`. Zero "zapomniałeś zamknąć połączenie". Zero dramatu.

### Co JdbcTemplate robi za ciebie?

1.  ~={8}Zarządza zasobami.=~ Otwiera, zamyka, sprząta - ty nie ruszasz palcem.
2. ~={8} Upraszcza zapytania.=~ `query, queryForObject, update, batchUpdate...`
3.  ~={8}Mapuje wyniki.=~
	- RowMapper
	- BeanPropertyRowMapper (mapper leniwy jak developer po jednym piwie)
	- lambda: `(rs, rowNum) -> new User(rs.getLong("id"), ...)`
4.  ~={8}Wspiera batch inserts.=~ I to szybko. Dużo szybciej niż ORM na dużej ilości danych.

### Po co nam JdbcTemplate, skoro mamy JPA?

JPA nie radzi sobie z każdym przypadkiem - szczególnie z masowymi operacjami lub ultra custom SQL.
JdbcTemplate jest szybsze tam, gdzie ORM dławi się bardzo szybko.
Masz pełną kontrolę nad SQL-em - żadnych magicznych generatorów zapytań.

Spring dokumentuje to jako jeden z podstawowych sposób dostępu do danych obok JPA.

```java
public record User(Long id, String name) { }
```
![[Pasted image 20251210110937.png]]

![[Pasted image 20251210111015.png]]

![[Pasted image 20251210111034.png]]