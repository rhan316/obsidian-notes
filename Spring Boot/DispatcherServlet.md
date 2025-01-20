`DispatcherServlet` to serce mechanizmu Spring MVC. Jest to pojedynczy serwlet zarejestrowany w kontenerze serwletów (np. Tomcacie), który przejmuje wszystkie żądania skierowane do aplikacji i zarządza ich obsługą.

---
***Jak działa DispatcherServlet?***
Gdy użytkownik wysyła żądanie HTTP, np. `GET /api/users`, oto co dzieje się za kulisami:

**Żądanie trafia do Tomcata** - Tomcat przekazuje żądanie do serwletu zarejestrowanego na określonej ścieżce (np. `/`).

**DispatcherServlet przejmuje kontrolę** - Analizuje żądanie i decyduje, który komponent aplikacji (np. metoda kontrolera) powinien obsłużyć.

**Routing i wywoływanie metody kontrolera** - `DispatcherServlet` korzysta z mapowania URL (np. `/api/users/`) zdefiniowanego w kontrolerach za pomocą adnotacji takich jak `@RequestMapping` lub `@GetMapping`. Przekazuje żądanie do odpowiedniej metody kontrolera.

**Przetwarzanie odpowiedzi** - Po wykonaniu logiki biznesowej metody kontrolera zwraca wynik (np. JSON), który jest formatowany i zwracany jako odpowiedź HTTP.

---
DispatcherServlet jest kluczowym elementem Spring MVC, zapewniającym centralny punkt obsługi żądań HTTP. W Spring Boot jego rejestracja i konfiguracja są automatyzowane, co upraszcza tworzenie aplikacji webowych. Mechanizm ten wspiera elastyczność, wydajność i centralizację w przetwarzaniu żądań.
