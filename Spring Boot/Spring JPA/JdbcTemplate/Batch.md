
***Co to jest batch?***

To sposób wykonywania wielu SQL-i na raz, w jednym strzale do bazy.
Dlaczego? -> Szybciej, mniej overheadu, mniej połączeń, baza nie dostaje depresji od miliona pojedynczych INSERT-ów.

Wygląda jak cheat code na wydajność.

### BatchUpdate z JdbcTemplate

Jeśli masz listę np. 1_000 albumów i chcesz je dodać hurtowo:
```java
String sql = "INSERT INTO albums (Title, ArtistId) VALUES (?, ?)";

jdbcTemplate.batchUpdate(sql, albums, albums.size(), (ps, album) -> {
	ps.setString(1, album.getTitle());
	ps.setLong(2, album.getArtistId());
});
```
szybko, stabilnie, elegancko, nie zwraca wygenerowanych kluczy (bo JDBC tak działa - deal with it).

### Batch z NamedParameterJdbcTemplate

Tak, też można - wygląda brzydziej, ale działa:
```java
String sql = "INSERT INTO albums (Title, ArtistId) VALUES (:title, :artistId)";

List<MapSqlParameterSource> batch = albums.stream()
	.map(a -> new MapSqlParameterSource()
			.addValue("title", a.getTitle())
			.addValue("artistId", a.getArtistId()))
		.toList();
		
namedParameterJdbcTemplate.batchUpdate(sql, batch.toArray(new SqlParameterSource[0]));
```
działa z nazywanymi parametrami, łatwiej czytać, nadal brak wygenerowanych ID

![[Pasted image 20251212161342.png]]
