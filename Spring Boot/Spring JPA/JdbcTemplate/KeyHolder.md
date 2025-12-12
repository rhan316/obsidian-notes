
JDBC nie zwraca ID wygenerowanego przez bazę danych, jeśli sam o to nie poprosisz.
`GeneratedKeyHolder` to po prostu implementacja KeyHoldera.

### Jak to działa?

1. Piszesz `jdbcTemplate.update(...)`
2. Spring tworzy PreparedStatement w trybie "daj mi klucze zwrotne"
3. Baza generuje ID (np. auto-increment)
4. Spring pakuje klucze do `GeneratedKeyHolder`
5. Ty je z niego wyciągasz jak batonik z automatu.

```java
String sql = "INSERT INTO user (name, email) VALUES (?, ?)";
KeyHolder keyHolder = new GeneratedKeyHolder();

jdbcTemplate.update(conn -> {
	var ps = conn.prepareStatement(sql, new String[]{"id"});
	ps.setString(1, "Courtney");
	ps.setString(2, "invisigal@sdn.org");
	
	return ps;
}, keyHolder);
```

#### Dlaczego musisz podać nazwę kolumny?

Baza może generować więcej niż jeden klucz. Albo Spring nie ma jasnej informacji, który chcesz.
Tak, wiem, to irytujące.
Tak, musisz to pisać ręcznie.
Tak, wszyscy tak robią.

- **KeyHolder** → pojemnik na wygenerowane ID.
    
- **GeneratedKeyHolder** → standardowa implementacja.
    
- **Spring** → robi syfiastą robotę JDBC za ciebie.
    
- **Ty** → przestajesz błądzić w ciemnościach jak idiota.

![[Pasted image 20251212094612.png]]
Ten kod mówi:
„Wykonaj INSERT, poproś bazę o wartość wygenerowanej kolumny `id`, a wynik włóż do `keyHolder`.”

Zależnie od typu klucza:
```java
np.
Long id = keyHolder.getKey().longValue();

jeśli klucz jest wartością UUID:

UUID id = UUID.fromString((String) kh.getKeys().get("id"));
```
