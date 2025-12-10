Spring od lat daje dwa "szablonowe" narzędzia do prostych operacji:
`SimpleJdbcInsert` -> insertujesz dane.
`SimpleJdbcCall` -> wywołujesz procedury składowane

I nie, to nie jest konkurencja dla JdbcTemplate/JdbcClient.
**To wyższy poziom abstracji, kiedy nie chcesz pisać:** 
`INSERT INTO users (name, age) VALUES (?, ?)`
albo gdy w ogóle masz procedury typu `sp_register_user`.

#### `SimpleJdbcInsert` - INSERT bez SQL-a

Wstawiasz rekord bez ręcznego pisania: SQL, nazw kolumn, klucza generowanego.

Jak z tego korzystać?
```java
SimpleJdbcInsert insert =
	new SimpleJdbcInsert(dataSource)
		.withTableName("users")
		.usingGeneratedKeyColumns("id");
```

A kiedy chcesz wstawić dane:
```java
Map<String, Object> params = Map.of(
	"name", "Courtney",
	"age", 27
);

Number id = insert.executeAndReturnKey(params);
```

![[Pasted image 20251210115211.png]]

#### `SimpleJdbcCall` - procedury składowane bez płaczu

Tak, wiem. Procedury.
Brzmi jak trauma z Oracle'a z 2009.
Ale są projekty, gdzie procedury to fundament.

**SimpleJdbcCall** pozwala wywołać je bez ręcznego pisania:
- `CallableStatement`
- rejestracji parametrów IN/OUT
- typów danych

Np.
```java
SimpleJdbcCall call =
	new SimpleJdbcCall(dataSource)
		.withProcedureName("add_customer")
```

Wywołanie:
```java
Map<String, Object> result = call.execute(
	Map.of(
		"name", "Courtney",
		"age", 27
	)
);
```

![[Pasted image 20251210115544.png]]


