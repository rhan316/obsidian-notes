Ciasteczka, czyli HTTP Cookies, są niewielkimi fragmentami danych, które serwer wysyła do przeglądarki użytkownika w odpowiedzi na żądanie HTTP. Te dane są następnie przechowywane w przeglądarce i wysyłane z powrotem do serwera przy każdym kolejnym żądaniu, jeśli spełniają określone warunki. W kontekście aplikacji Spring Boot oraz sesji HTTP, ciasteczka pełnią kluczową rolę w utrzymaniu stanu użytkownika, np. zarządzaniu sesjami.

Wyobraźmy sobie, że odwiedzasz kawiarnię i dostajesz kartę lojalnościową (ciasteczko). Na tej karcie zapisane jest Twoje imię i specjalny kod identyfikacyjny. Za każdym razem, gdy wracasz do tej samej kawiarni, pokazujesz swoją kartę, a obsługa od razu wie, kim jesteś, jakie kawy lubisz i ile pieczątek masz na karcie. Nie muszą Cię pytać o wszystko od nowa za każdym razem - Twoja karta (ciasteczko) przechowuje te informacje.
Podobnie działa ciasteczko w protokole HTTP:
1. **Serwer wysyła ciasteczko do przeglądarki** - Przy pierwszym żądaniu serwer może powiedzieć przeglądarce, żeby przechowywała ciasteczko z unikalnym identyfikatorem sesji (np. JSESSIONID w Spring Boot).
2. **Przeglądarka przechowuje ciasteczko** - To ciasteczko jest zapisywane w pamięci przeglądarki i jest przypisane do domeny, z której pochodzi (np. example.com)
3. **Przeglądarka wysyła ciasteczko przy kolejnych żądaniach** - Gdy użytkownik wysyła kolejne żądanie do tej samej domeny, ciasteczko jest dołączane do nagłówka HTTP. Dzięki temu serwer wie, że żądanie pochodzi od tego samego użytkownika.

---
W Spring Boot ciasteczka są często wykorzystywane do zarządzania sesjami użytkownika. Sesja HTTP to sposób na utrzymanie informacji o użytkowniku pomiędzy żądaniami w statelessowym protokole HTTP (protokół ten z założenia nie "pamięta" wcześniejszych interakcji).

**Przebieg z użyciem ciasteczka sesyjnego**
1. **Pierwsze żądania** - Kiedy użytkownik wysyła pierwsze żądanie, serwer tworzy nową sesję (np. obiekt `HttpSession` w Spring Boot). W jej ramach można przechowywać dane użytkownika, np. login, role czy inne informacje.
2. **Ciasteczko z identyfikatorem sesji** - Serwer generuje ciasteczko (np. `JSESSIONID`) z unikalnym identyfikatorem tej sesji i wysyła je do przeglądarki.
3. **Kolejne żądania** - Przeglądarka przesyła ciasteczko w każdym kolejnym żądaniu, dzięki czemu serwer może odnaleźć wcześniej utworzoną sesji i skojarzyć ją z użytkownikiem.

---
***Kluczowe cechy ciasteczek**
1. **Klucz i wartość**: Ciasteczka są przechowywane w formacie klucz-wartość, np. `JSESSIONID=abc123`.
2. **Czas życia**: Sesyjne ciasteczka (domyślne w SB) znikają po zamknięciu przeglądarki. Trwałe ciasteczka mają określoną datę wygaśnięcia `max-age` lub `Expires`.
3. **Domena i ścieżka**: Ciasteczka są przypisane do konkretnej domeny i ścieżki, co oznacza, że będą wysyłane tylko do serwera, z którego pochodzą.
4. **Bezpieczeństwo**: *Secure* - wysyłane tylko przez HTTPS, *HttpOnly* - niedostępne dla JS (chroni przed atakami XSS), *SameSite* - ogranicza wysyłanie ciasteczek do zapytań z tej samej strony (chroni przed atakami CSRF).

---
Ciasteczka pozwalają aplikacjom webowym przechowywać kontekst użytkownika w świecie, w którym protokół HTTP jest "bezwładny" stateless. Dzięki czemu aplikacje mogą:
- Utrzymywać użytkownika zalogowanego.
- Zapamiętywać jego preferencje.
- Personalizować treści.