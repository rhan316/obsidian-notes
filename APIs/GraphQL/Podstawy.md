GraphQL = schema-first.

To znaczy:
- zanim napiszesz linijkę kodu, musisz mieć diagram, typy, relacje, co zwraca co.
- Schema definiuje:
1. Query (pobieranie)
2. Mutation (modyfikowanie)
3. Subscription (push eventów)
4. Type'y (obiekty, enumy, inputy)

```ts
type Query {
	users: [User]
}

type Mutation {
	createUser(input: CreateUserInput!): User!
}

type User {
	id: ID!
	name: String!
}
```

### Resolver = funkcja, która faktycznie robi robotę

Schema to ładny papierek.
Resolver to brudny backend, który faktycznie robi:
- query do bazy
- walidację
- logikę biznesową
- sprawdzanie uprawnień

Resolver to:
```js
const resolvers = {
	Query: {
		users: () => db.users.findAll()
	}
}
```
Czyli: "Kiedy ktoś zapyta o users" -> wykonaj tę funkcję.
Proste jak twoje wymówki.

### GraphQL NIE JEST ORM-em

To nie jest magiczna maszynka, która sama wie, jak działa twój system.

Chcesz jednego użytkownika?
Musisz sam napisać, jak go pobrać.

Chcesz powiązane dane?
Musisz powiedzieć, skąd je brać.

Nie ma żadnego "daj całą bazę i ogarnij", bo wtedy stworzysz potwora.

### N+1 problem - i tak, dotyczy cię to natychmiast

GraphQL jest cudowny... dopóki nie zauważysz, że zrobiłeś tysiąc zapytań do bazy jednym requestem, geniuszu.

Np.

1. Query pobiera listę userów
2. Każdy user ma pole `posts`
3. Klient prosi o `users { posts { title } }`
4. Ty: "hehe, dam prosty resolver"
5. Resolver robi 1 zapytanie o userów, a potem... jedno zapytanie o posty na każdego usera.
Gratulacje użytkowniku, masz N+1.

Rozwiązanie:
- DataLoader
- batching
- cache per request
Jak tego nie ogarniesz, backend ci spłonie.

### Input types - bo Mutation nie bierze miliarda argumentów

Mutation z tysiącem argumentów to zbrodnia.
Zawsze rób inputy:
```js
input CreateUserInput {
	name: String!
	email: String!
}
```
I nie pytaj "czy można bez inputa" - można, tak samo jak skakać na główkę do pustego basenu.

### Pagination - GraphQL nie da ci jej sam

Chcesz listy?
Musisz zrobić: offset/limit lub cursor-based
Bo inaczej klient poprosi o 100k rekordów i twój serwer powie "ja pierdolę".

### Error handling - błędy to też dane

GraphQL nie rzuca 500-tkami "bo tak".
Błędy lecą w osobnym polu:
```json
{
	"data": null,
	"errors": [{ ... }]
}
```
Musisz sam zdecydować:
 - co jest błędem biznesowym
 - co zwracasz jako null
 - co rzucasz jako wyjątek

### Autoryzacja - GraphQL to nie REST, nie chowasz się za endpoitem

REST: `/admin/delete-user`
GraphQL: jedna brama, jeden endpoint

Więc:
- autoryzacja = na resolverach
- albo używasz czegoś jak graphql-shield
- albo piszesz własny middleware
Jak tego nie zrobisz -> gratki, wszyscy mają dostęp do wszystkiego.

### Nie rób jednego wielkiego root Query

Query z 300 polami?
To nie API.
To czyściec.
Podziel wszystko na moduły: `Query: user, product, payment`

### GraphQL jest dla klientów - nie dla ciebie

To klient decyduje, co chce.
Twoim zadaniem jest to umożliwić, ale nie pozwolić mu cię zabić.