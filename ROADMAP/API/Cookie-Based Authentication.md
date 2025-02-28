Metoda uwierzytelnienia, w której serwer przechowuje sesję użytkownika i wysyła przeglądarce specjalny plik cookie, służący do potwierdzenia tożsamości użytkownika przy kolejnych żądaniach.

***Użytkownik loguje się do aplikacji***
Przeglądarka wysyła dane logowania `username + password` do serwera w żądaniu HTTP POST.
```http
POST /logun HTTP/1.1
Host: example.com
Conent-Type: application/json

{
	"username": "john_doe",
	"password": "supersecret"
}
```

***Serwer weryfikuje dane i tworzy sesję***
Serwer sprawdza poprawność danych logowania (np. w bazie danych).
Tworzy sesję użytkownika i zapisuje jej ID w pamięci (np. Redis, baza danych, pamięć RAM).
Generuje plik cookie z identyfikatorem sesji i wysyła go do przeglądarki.
```http
HTTP/1.1 200 OK
Set-Cookie: session_id=abc123; HttpOnly; Secure; SameSite=Strict
```

***Przeglądarka przechowuje cookie***
Przeglądarka zapisuje cookie `session_id=abc123`.
Cookie jest automatycznie wysyłane do serwera przy każdym kolejnym żądaniu.
```http
GET /dashboard HTTP/1.1
Host: example.com
Cookie: session_id=abc123
```

***Serwer sprawdza cookie i autoryzuje użytkownika***
Serwer otrzymuje cookie i sprawdza, czy `session_id=abc123` istnieje w systemie.
Jeśli sesja jest ważna serwer rozpoznaje użytkownika i zwraca mu odpowiednie zasoby.
Jeśli sesja wygasła lub jest niepoprawna -> użytkownik jest przekierowany na stronę logowania.
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"username": "john_doe",
	"role": "admin"
}
```

***Wylogowanie użytkownika***
Kiedy użytkownik się wyloguje, serwer usuwa sesję a cookie staje się bezużyteczne.
Serwer może również nakazać przeglądarce usunięcie cookie:
`Set-Cookie: session_id=; Expires=Thu; 01 Jan 1970 00:00; HttpOnly; Secure`