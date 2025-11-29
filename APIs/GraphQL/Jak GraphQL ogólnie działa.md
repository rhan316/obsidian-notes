Powiedzmy, że masz użytkowników, ich listę znajomych i posty.
W REST musiałbyś latać po różnych endpointach jak dzieciak po sklepie ze słodyczami.

A w GraphQL piszesz:
```javascript
query {
	user(id: 42) {
		name
		email
		friends { name }
	}
		posts(limit: 2) { title createdAt }
}
```
I backend odpowiada:
```json
{
  "data": {
    "user": {
      "name": "Ktoś Tam",
      "email": "test@example.com",
      "friends": [
        { "name": "Janek" },
        { "name": "Ola" }
      ],
      "posts": [
        {
          "title": "Mój pierwszy post",
          "createdAt": "2024-02-10"
        },
        {
          "title": "Drugi post",
          "createdAt": "2024-03-01"
        }
      ]
    }
  }
}
```
Tyle. Nic więcej. Zero śmieci. Zero nadmiaru. Zero "proszę pana, gdzie jest endpoint do....?"
