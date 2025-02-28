**JSON** oznacza JavaScript Object Notation jest formatem tekstowym do przesyłania danych przez aplikacje internetowe. Przechowuje informacje w łatwy sposób. Każdy język programowania może z niego korzystać, co skutkuje wysoką popularnością.

**Token** to ciąg danych reprezentujący daną wartość, np. tożsamość użytkownika. Serwer pobiera taki token i sprawdza czy jest on prawidłowy (np. za pomocą kluczy, certyfikatów).

**JWT** - JSON Web Token - Wykorzystuje się do transferu danych między podmiotami, szczególnie w celach uwierzytelnienia i autoryzacji.
Składa się z 3 elementów: **XXXXX.YYYYYYYY.ZZZZ**
- **X** -> nagłówek w formacie JSON zawierający algorytm oraz typ tokena. `{"alg": "HS256", "type": "JWT"`
-  **Y** -> ładunek w formacie JSON zawierający tak zwane roszczenia, czyli zawartość tokena (payload) zawierający dane do przesłania.
- **Z** -> sygnatura podpisująca token i pozwalająca na weryfikację jego autentyczności.

Zalety JWT Token:
- Niezależne od stanu sesji na serwerze - serwer nie musi przechowywać żadnych informacji o sesjach użytkowników.
- Kompaktowy format.
- Bezpieczeństwo - dzięki wykorzystaniu zaawansowanych algorytmów szyfrowania.