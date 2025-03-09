**CORS, czyli Cross-Origin Resource Sharing**, to mechanizm bezpieczeństwa w przeglądarkach internetowych, który kontroluje, w jaki sposób aplikacje webowe działające w jednej domenie (origin) mogą żądać zasobów z innych domeny. Jest to ważne ze względu na **politykę tego samego źródła (Same-Origin Policy, SOP)**, która ogranicza skrypty JavaScript do wykonywania żądań między różnymi domenami.

*Domena* -> to unikalna nazwa, która identyfikuje stronę internetową lub serwer w sieci. Domena jest częścią adresu URL (Uniform Resource Locator), który użytkownicy wpisują w przeglądarce, aby uzyskać dostęp do strony internetowej. Domena pełni rolę przyjaznej dla człowieka etykiety, która zastępuje trudne do zapamiętania adresy IP.

### Co to jest CORS?

**Same-Origin Policy (SOP)**
Przeglądarki domyślnie blokują żądania między różnymi (originami), aby zapobiec atakom, takim jak **Cross-Site Request Forgery (CSRF)**.
Origin jest definiowany jako kombinacja protokołu (HTTP/HTTPS), hosta (domeny) i portu. Np.
- `https://example.com` i `http://example.com` to różne originy (różne protokoły).
- `https://example.com` i `https://api.example.com` to różne originy (różne hosty).
- `https://example.com:80` i `https://example.com:443` to różne originy (różne porty).

**CORS**
CORS to mechanizm, który pozwala serwerom na kontrolowanie, które zewnętrzne domeny mogą uzyskać dostęp do ich zasobów. Serwer może wysyłać specjalne nagłówki HTTP, aby zezwolić na żądania z określonych domen.

