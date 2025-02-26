*Cache* to mechanizm przechowywania często używanych danych w szybkiej pamięci, aby uniknąć ponownego pobierania lub obliczania tych samych informacji.

Dzięki cache możemy:
- Przyśpieszyć działanie aplikacji (mniej zapytań do bazy danych, szybsze ładowanie stron)
- Zmniejszyć obciążenie serwera (mniej operacji CPU, mniejszy ruch sieciowy)
- Zoptymalizować doświadczenie użytkownika (szybsze działanie aplikacji, mniejsze zużycie baterii w urządzeniach mobilnych)

### Rodzaje cache w web dev

***Cache przeglądarki (Browser Cache)***
Przeglądarka przechowuje statyczne zasoby `HTML, CSS, JS, obrazy` na dysku użytkownika.
Dzięki czemu kolejne wizyty na stronie są szybsze.
Konfigurowane przez nagłówki HTTP (`Cache-Control, Expires, ETag`)
```http
Cache-Control: max-age=86400, public
Expires: Wed, 21 Oct 2025
```

***Cache na serwerze (Server-Side Cache)***
Serwer zapisuje wygenerowaną stronę lub dane, aby uniknąć ich ponownego przetwarzania.
Może być stosowany na poziomie aplikacji (np. Redis, Memcached) lub proxy (np. Varnish, Nginx)
Przykłady:
Przechowywanie wyników zapytań do bazy w Redis (unikamy powtarzających się zapytań).
Cache'owanie całych stron HTML w Varnish (szybsze ładowanie stron).

***Cache bazy danych (Database Cache)***
Przechowywanie wyników często wykonywanych zapytań.
Pomaga zredukować liczbę operacji na bazie danych.
```java
// Sprawdź, czy wynik zapytania jest w Redis
String cachedData = redis.get("user:123");
if (cachedData != null) return cachedData;

// Jeśli nie ma w cache, pobierz z bazy i zapisz w Redis
String userData = database.query("SELET * FROM users WHERE id = 123");
redis.set("user123", userData, Duration.ofMinutes(10));
return userData;
```
Redis zmniejsza liczbę zapytań do MySQL, przyśpieszając aplikację.

***CDN Cache (Content Delivery Network Cache)***
CDN przechowuje statyczne pliki `JS, CSS, obrazy` blisko użytkownika.
Redukuje obciążenie serwera i skraca czas ładowania stron.
Przykład:
Użytkownik w EU pobiera obraz z serwera w USA -> CDN zapisuje obraz w EU -> kolejni użytkownicy w EU pobierają go szybciej.

***Application Cache (Cache w kodzie aplikacji)***
Cache na poziomie kod w aplikacjach webowych.
Przechowywanie wyników funkcji, obliczeń lub API reponses w pamięci.
```java
@Cacheable("users")
public User getUserById(long id) {
	return userRepository.findById(id).orElseThrow();
}
```
Spring automatycznie przechowa wynik w cache, eliminując kolejne zapytania do bazy danych!
