
### Schema - mózg operacji

Backend definiuje strukturę świata:
```json
type User {
	id: ID!
	name: String!
	email: String!
	friends: [User]
	posts(limit: Int): [Post]
}

type Post {
	title: String!
	createdAt: String!
}
```


### Query - twoje życzenie

Ty piszesz dokładnie czego chcesz.
Jakbym ja poszła do Blazera i powiedziała:
"Potrzebuję dwie rzeczy: sprzęt i spokój. Daj to, i nie pierdol się"
Tak działa GraphQL - dajesz listę życzeń.

### Resolvers - małe gremliny robią robotę

Każde pole z schemy ma swój resolver.
To funkcję, które mówią backendowi:
- skąd wziąć dane
- jak je połączyć
- co zwrócić
np.
```js
User: {
	posts: (parent, args, context) => {
		return db.posts.find({ userId: parent.id}).limit(args.limit);
	}
}
```

### GraphQL składa to w jedną odpowiedź

Ty dajesz zapytanie -> GraphQL wywołuje odpowiednie resolvery  -> buduje drzewko -> zwraca JSON
To jest eleganckie.