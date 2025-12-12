
To taki fajniejszy JdbcTemplate, który pozwala pisać zapytania  z nazywanymi parametrami, zamiast tych wkurwiających `?`

```sql
Zamiast tego:
INSERT INTO user (name, email) VALUES (?, ?)

Piszesz:
INSERT INTO user (name, email) VALUES (:name, :email)
```
Wygląda to wtedy bardziej naturalnie, a nie jak cyborg w trybie ASCII.

Istnieje to po to, aby programiści nie musieli zgadywać czy 3 `?` to email, username a może numer buta?
Nazywane parametry = koniec zgadywanki.