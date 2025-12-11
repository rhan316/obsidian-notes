Co to jest?
JdbcClient to takie połączenia *JdbcTemplate + NamedParameterJdbcTemplate*, tylko w wersji:
- płynnej
- krótszej
- prostrzej
- bardziej nowoczesnej
- i z Optional zamiast NullPointerException

**Płynny builder (coś jak JPA Query API, tylko do SQL)**
```java
client.sql("SELECT * FROM users WHERE ID = :id)
	.param("id", 3)
	.query(User.class)
	.optiional();
```

**Obsługuje named parameters, np. `:id`**

**Obsługuje positional parameters `?`**

**Mapowanie wyników przez:**
- `.query(Class)`
- row-mappery
- ResultSetExtractor
- wszystko, co znałeś z JdbcTemplate

To nie jest nowy silnik, tylko lukier do starego JdbcTemplate.

Do poważniejszych akcji jak batch, stored procedures - nadal używasz JdbcTemplate, SimpleJdbcInsert, SimpleJdbcCall.

![[Pasted image 20251210114117.png]]

![[Pasted image 20251210114133.png]]

![[Pasted image 20251210114152.png]]

![[Pasted image 20251210114212.png]]