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
Co to robi?
- woła resolver `createUser`
- tworzy użytkownika
- zwraca dokładnie te pola, o które prosiłeś
Tak, możesz tworzyć/modyfikować/usuwać dane i od razu decydować, co chcesz dostać w odpowiedzi. REST może tylko patrzeć z boku i płakać.

Mutacje:
- modyfikują stan (tworzą, aktualizują, kasują)
- zawsze są jawnie oznaczone jako `mutation`
- zwracają wartość po zmianie (GraphQL nie ma czegoś takiego jak typ `void`)

### Subskrypcje - czyli "daj mi znać, kiedy coś się wydarzy"
Subskrypcje to takie... podsłuchiwanie, ale nie w ten fajny sposób, tylko techniczny.
Działają na WebSocketach: **serwer pcha dane do klienta, kiedy coś się zmieni**.

Idealne do:
- powiadomień
- live chatów
- "ktoś właśnie zaktualizował dokument i masz konflikt, brawo"
- realtime dashboards
Np.
```graphql
subscription {
	userCreated {
		id
		name
	}
}
```
I za każdym razem, gdy nowy user powstaje - bam, dostajesz event bez odpytywania serwera milion razy jak idiota.


