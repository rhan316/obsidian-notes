*Normalizacja* to proces organizowania danych w bazie tak, aby zminimalizować redundancję i uniknąć problemów z integracją danych. Dzięki normalizacji unikamy sytuacji, w której te same informacje są przechowywane w wielu miejscach, co prowadzi do trudności w aktualizacji i błędów logicznych.

Wyobraź sobie, że prowadzisz sklep internetowy i trzymasz informacje o zamówieniach w jednej wielkiej tabeli, gdzie każda kolumna przechowuje wszystko o zamówieniu, użytkowniku i produktach.

| order_id | user_name     | user_email     | product_name | product_price | quantity |
| -------- | ------------- | -------------- | ------------ | ------------- | -------- |
| 1        | Jan Nowak     | jan@email.com  | Laptop       | 3_000         | 1        |
| 2        | Jan Nowak     | jan@email.com  | Myszka       | 100           | 1        |
| 3        | Anna Kowalska | anna@email.com | Klawiatura   | 200           | 1        |
**Problem:**
- Redundancja danych - dane użytkownika powtarzają się w każdej linii zamówienia.
- Trudność w aktualizacji - jeśli Jan Nowak zmieni e-mail, trzeba zmienić go w każdym zamówieniu!
- Problemy z integralnością - co jeśli w jednym zamówieniu Jan ma `jan@email.com`, a w innym `jan.nowak@email.com`?

**Rozwiązanie - Podział tabeli na mniejsze, powiązane ze sobą encje**

### Podstawowe poziomy normalizacji (1NF, 2NF, 3NF)
Normalizacja odbywa się w kilku etapach zwanych postaciami normalnymi (Normal Forms).

***1NF (Pierwsza postać Normalna) - eliminacja powtarzających się grup***
Zasada: Każda kolumna powinna zawierać tylko pojedyncze wartości (atomic data).
```sql
CREATE TABLE orders (
	order_id SERIAL PRIMARY KEY,
	user_name TEXT,
	user_email TEXT,
	products TEXT, -- "Laptop, myszka"
	prices TEXT -- "3_000, 100"
)
```
Tutaj mamy wiele produktów w jednej kolumnie, co jest złe, ponieważ nie możemy łatwo wyszukiwać ani sortować po produktach.

*Poprawiona wersja (1NF)*
```sql
CREATE TABLE orders (
	order_id SERIAL PRIMARY KEY,
	user_name TEXT,
	user_email TEXT,
	product_name TEXT,
	product_price NUMERIC
) -- Rozbiliśmy produkty na osobne wiersze, zamiast trzymać ich listę w jednej kolumnie
```

***2NF (Druga Postać Normalna) - Eliminacja zależności częściowych***
Zasada: Każda kolumna musi zależeć od całego klucza głównego, a nie tylko jego części.
*Błąd w 1NF*:
- `user_name` i `user_email` zależą tylko od użytkownika, a nie od konkretnego zamówienia.
- Jeśli ten sam użytkownik zrobi wiele zamówień, jego dane powtarzają się wiele razy.

*Rozwiązanie 2NF - Podział tabel na encje*
```sql
CREATE TABLE users (
	user_id SERIAL PRIMARY KEY,
	name TEXT,
	email TEXT UNIQUE
);

CREATE TABLE orders (
	order_id SERIAL PRIMARY KEY,
	user_id INT REFRENCES users(user_id)
); -- Teraz mamy osobną tabelę users, a orders przechwuje tylko identyfikator użytkownika
``` 