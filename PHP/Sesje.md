Sesje w PHP to mechanizm umożliwiający przechowywanie informacji o użytkowniku podczas jego interakcji z aplikacją internetową. W przeciwieństwie do **cookies**, które są przechowywane po stronie klienta (w przeglądarce), sesje przechowują dane na serwerze i identyfikują użytkownika za pomocą unikalnego identyfikatora sesji (session ID), przesyłanego do przeglądarki jako cookie.

**Jak działają sesje w PHP?**

1. **Rozpoczęcie sesji** - PHP tworzy unikalne ID sesji i zapisuje je w supergloblanej tablicy `$_SESSION` po stronie serwera.
2. **Przechowywanie danych sesji** - Możemy przypisać wartości do `$_SESSION`, aby przechowywać dane, np. login użytkownika.
3. **Wykorzystywanie ID sesji** - ID sesji jest przekazywane do użytkownika w ciasteczku (`PHPSESSID`) lub URL (w trybie transparentnym).
4. **Odczyt i modyfikacja danych sesji** - W dowolnym miejscu skryptu PHP możemy odczytać wartości zapisane w `$_SESSION`.
5. **Zakończenie sesji** - Możemy ręcznie usunąć sesję lub zamknąć ją po stronie serwera, aby dane użytkownika zostały usunięte.

---
**Startowanie sesji**
Przed użyciem zmiennych sesji należy ją uruchomić za pomocą `session_start()`
```
session_start(); // Rozpoczyna sesję lub wznawia istniejącą
$_SESSION['username'] = 'JanKowalski'; // Przypisanie wartości do sesji
echo 'Zalogowany jako: ' . $_SESSION['username'];
```
`session_start()` musi być wywołane na początku skryptu (przed wysłaniem jakiegokolwiek HTML-a).

**Odczyt danych z sesji**
Po zalogowaniu użytkownika możemy na innej stronie odczytać przechowywane dane
```
session_start();
if (isset($_SESSION['username'])) {
	echo "Witaj, " . $_SESSION['username'] . "!";
} else {
	echo "Nie jesteś zalogowany.";
}
```

**Usunięcie sesji**
Jeśli użytkownik się wyloguje, możemy usunąć sesję
```
session_start();
session_unset(); // Usuwa wszystkie zmienne sesji
session_destroy(); // Niszczy sesję na serwerze
echo "Sesja zakończona.";
```


**Gdzie przechowywane są dane sesji?**
PHP domyślnie przechowuje sesje jako pliku w katalogu systemowym (np. `/tmp` w systemach Linux). Można to sprawdzić w pliku `php.ini` .


**Jak działa ID sesji?**
PHP generuje unikalne ID sesji.
ID sesji jest przesyłane do użytkownika jako ciasteczko `PHPSESSID`.
Przy każdej wizycie przeglądarka przesyła `PHPSESSID` do serwera, który wznawia sesję.
```
session_start();
echo session_id(); // Pobiera ID sesji
session_regenerate_id(true); // Regeneruje ID sesji dla bezpieczeństwa
```

**Bezpieczeństwo sesji**

1. *Nie przechowuj w sesji haseł!* Lepiej przechowywać tylko `user_id`, a pełne dane pobierać z bazy.
2. *Regeneracja ID sesji* Zapobiega przechwyceniu sesji przez ataki *session hijacking*.
	`session_regenerate_id(true);` 
3. *Ograniczenie dostępu do ciasteczek sesji* - Można ustawić flagę `HttpOnly` i `Secure`, aby zapobiec atakom XSS.
```
session_set_cookie_params([
	'lifetime' => 0, // Sesja wygasa po zamknięciu przeglądarki
	'path' => '/',
	'domain' => '',
	'secure' => true, // Wymaga HTTPS
	'httponly' => true, // Blokuje dostęp JavaScriptu
	'samesite' => 'Strict' // Chroni przed atakami CSRF
])
```