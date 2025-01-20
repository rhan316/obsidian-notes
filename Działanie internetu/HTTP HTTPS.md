**HTTP (Hyper Text Transfer Protocol)** to protokół komunikacyjny używany do przesyłania danych między klientem (np. przeglądarką) a serwerem.

**Warstwa aplikacji** - HTTP działa na poziomie aplikacyjnym w stosie protokołów TCP/IP.

**Bezstanowy protokół** - Nie przechowuje informacji o poprzednich żądaniach (każde żądanie jest niezależne). Mechanizmy takie jak *cookies*, *session*, *local storage* są używane do utrzymania stanu.

---
***Jak działa HTTP?***
1. Podstawowy przepływ:
	- Klient wysyła żądanie HTTP do serwera.
	- Serwer przetwarza żądanie i zwraca odpowiedź HTTP (np. dokument HTML, dane JSON).
2. Metody HTTP: Metody te definiują rodzaj operacji, jakie klient chce wykonać na serwerze:
	- *GET* - pobieranie danych (np. stron HTML).
	- *POST* - wysyłanie danych na serwer (np. formularze).
	- *PUT* - Aktualizacja danych na serwerze.
	- *DELETE* - Usuwanie zasobów.
	- *HEAD* - pobiera tylko nagłówki odpowiedzi (bez treści).
	- *OPTIONS* - sprawdza obsługiwane metody dla danego zasobu.
3. Kody statusu HTTP:
	- 2xx (sukces): `200: ok`, `201: created`
	- 3xx (przekierowanie): `301: Moved Permanently`, `302: Found`
	- 4xx (błąd klienta) `400: Bad Request`, `401: Unauthorized`, `404: Not Found`
	- 5xx (błąd serwera) `500: Internal Server Error`, `503: Service Unavaiilable`
---
***Co to jest HTTPS?**

HTTPS (HTTP Secure) to bezpieczna wersja protokołu HTTP, która wykorzystuje TLS (Transport Layer Security) lub SSL (Secure Sockets Layer) do szyfrowania danych przesyłanych między klientem a serwerem.
HTTPS zapewnia:
**Szyfrowanie** - dane są zaszyfrowane, co uniemożliwia ich przechwycenie.
**Integralność danych** - dane nie mogą zostać zmienione podczas przesyłania.
**Uwierzytelnienie** - certyfikaty SSL/TLS potwierdzają tożsamość serwera.

---

| Funkcja        | HTTP                             | HTTPS                                             |
| -------------- | -------------------------------- | ------------------------------------------------- |
| Bezpieczeństwo | Brak szyfrowania (dane są jawne) | Dane są szyfrowane protokołem TLS/SSL             |
| Port domyślny  | 80                               | 443                                               |
| Certyfikat     | Nie wymaga certyfikatu           | Wymaga certyfikatu SSL/TLS                        |
| Wydajność      | Mniej zasobożerne                | Minimalnie wolniejsze (ze względu na szyfrowanie) |

---
***Przykład odpowiedzi HTTP***
```
HTTP/1.1 200 OK
Date: Thu, 16 Jan 2025 10:00:00 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 137

<html>
    <body>
        <h1>Hello, John!</h1>
    </body>
</html>

HTTP/1.1 404 Not Found
Date: Thu, 16 Jan 2025 10:05:00 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 88

<html>
    <body>
        <h1>404 Not Found</h1>
        <p>The requested resource was not found on this server.</p>
    </body>
</html>

```
Klient - serwer
```
GET /api/users HTTP/1.1
Host: api.example.com
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 68

[
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
]
```