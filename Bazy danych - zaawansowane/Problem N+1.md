Problem N+1 zapytań to klasyczny problem wydajnościowy występujący w aplikacjach korzystających z baz danych SQL. Występuje on wtedy, gdy zamiast jednego dobrze zoptymalizowanego zapytania, aplikacja wykonuje wiele małych zapytań, co prowadzi do drastycznego obniżenia wydajności.

#### Techniczny przykład w SQL

Załóżmy, że mamy dwie tabele:
1. `users` -> przechowuje informacje o użytkownikach
2. `orders` -> przechowuje zamówienia użytkownika, powiązane z kluczem obcym `user_id`

Teraz, jeśli chcemy pobrać listę użytkowników wraz z ich zamówieniami, możemy popełnić krytyczny błąd N+1:

***Błąd N+1 w kodzie aplikacji***
W wielu frameworkach ORM (np. Hibernate) kod może wyglądać tak:
```java
List<User> users = entityManager.createQuery("SELECT u FROM User u", User.class).getResultList;

for (User user : users) {
	print("User:" + user.getName());
	print("Orders: " + user.getOrders().size()); // <-- Hibernate wykona dodatkowe zapytanie dla każdego użytkownika!
}
```
**Co tu się dzieje?**

Hibernate wykonuje pierwsze zapytanie, aby pobrać użytkowników:
```sql
SELECT * FROM users;
```
Następnie, dla każdego użytkownika, osobno pobiera jego zamówienia:
```sql
SELECT * FROM orders WHERE user_id = 1;
SELECT * FROM orders WHERE user_id = 2;
SELECT * FROM orders WHERE user_id = 3;
SELECT * FROM orders WHERE user_id = 4;
-- i tak dalej dla N użytkowników...
```
Efekt? N+1 zapytań (1 do pobrania użytkowników + N do pobrania zamówień). Jeśli mamy 1000 użytkowników, to wykonamy 1001 zapytań - katastrofa wydajnościowa!
### Jak unikać problemu N+1 w Hibernate?

**Rozwiązanie 1: Fetch Join w JPQL**
Możemy użyć JOIN FETCH, aby pobrać użytkowników razem z ich zamówieniami.
```java
List<User> users = entityManager.createQuery(
	"SELECT u FROM User u JOIN FETCH u.orders", User.class
).getResultList();
```
Teraz Hibernate wykona jedno optymalne zapytanie:
```sql
SELECT u.*, o.* FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```
Wszystko jest pobierane jednym zapytaniem, eliminując problem N+1!

**Rozwiązanie 2: `@EntityGraph`**
Możemy użyć *EntityGraph*, aby poinformować Hibernate, że chcemy pobrać użytkowników razem z zamówieniami.
```java
@EntityGraph(attributePaths = {"orders"})
List<User> users = ... query ...
	.setHint("jakarta.persistence.fetchgraph", entityGraph)
	.getReusultList();
```
To pozwala uniknąć problemu N+1 bez modyfikowania zapytań.

**Rozwiązanie 3: `@BatchSize` w Hibernate**
Jeśli nie chcemy zmieniać zapytań, możemy powiedzieć Hibernate, aby pobierał zamówienia w paczkach:
*Dodajemy `@BatchSize` do `orders` w encji `User`*
```java
@OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
@BatchSize(size = 10) // pobiera zamówienia dla 10 użytkowników na raz
private List<Order> orders;
```
Zamiast N osobnych zapytań, Hibernate wykona mniej zapytań, np.:
```sql
SELECT * FROM orders WHERE user_id IN (1,2,3,4,5,6,7,8,9,10);
SELECT * FROM orders WHERE user_id IN (11,12,13,14,15,16,17,18,19,20);
```
Co drastycznie zwiększa wydajność.

#### Podsumowanie
Problem N+1 występuje, gdy Hibernate wykonuje osobne zapytania dla każdego obiektu w kolekcji.
Rozwiązania:
1. *JOIN FETCH* - użycie `JOIN FETCH` w JPQL.
2. *@EntityGraph* - predefiniowane zapytania do ładowania relacji.
3. *@BatchSize* - pobieranie danych w większych paczkach.