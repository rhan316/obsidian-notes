W GraphQL masz trzy główne operacje:
- `query` - pobieranie danych (czyli daj mi to)
- `mutation` - zmiana danych (czyli zrób coś)
- `subscription` - nasłuchiwanie na zmiany (powiadom mnie, kiedy coś się stanie)

Przykład mutacji
```json
mutation {
	createUser(name: "Jan", email: "jan@example.com") {
		id
		name
		email
	}
}
```
