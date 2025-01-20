Apache Tomcat to serwer aplikacyjny (a dokładniej serwer kontenerowy) przeznaczony głównie do obsługi aplikacji napisanych w języku Java, które korzystają z technologii takich jak *Servlets*, *JavaServer Pages (JSP)* i *WebSocket*. W kontekście **Spring Boot i Spring Framework**,~={green} Tomcat jest kluczowym narzędziem, które umożliwia uruchamianie aplikacji webowych=~.

---
***Czym jest Tomcat?***
Tomcat to tzw. **serwer kontenerowy (ang. servlet container)**. Jego głównym zadaniem jest obsługa aplikacji zgodnych z Java Servlet API. Możesz go traktować jako:
1. *Pośrednika*: Przyjmuje żądania HTTP, przekazuje je do odpowiednich komponentów aplikacji (np. kontrolerów w Springu), a następnie zwraca odpowiedź do klienta (np. przeglądarki).
2. *Silnik aplikacji webowej:* Zapewnia środowisko, w którym mogą działać aplikacje oparte na servletach i JSP.
**Kluczowe zadania Tomcata:**
- ~={8}Obsługa żądań HTTP=~: Tomcat działa jak kelner w restauracji. Odbiera zamówienia (żądania HTTP), przekazuje je do kucharza (Twojego kodu aplikacji), a następnie przynosi gotowe danie (odpowiedź HTTP).
- ~={magenta}Zarządzanie cyklem życia serwletów=~: Ładuje klasy serwletów, kiedy są potrzebne. Inicjalizuje, obsługuje i niszczy serwlety zgodnie z potrzebami.
- ~={yellow}Hostowanie aplikacji webowych=~: Tomcat umożliwia wdrażanie aplikacji w postaci plików **WAR (Web Application Archive).

---
***Jak Tomcat działa pod maską?***

**Przyjęcie żądania:** Kiedy użytkownik otwiera stronę w przeglądarce, np. `http://example.com` przeglądarka wysyła żądanie HTTP do serwera.

**Przekazanie do odpowiedniego komponentu:** Tomcat analizuje ścieżkę żądania (np. `/login`) i przekazuje je do odpowiedniego serwletu lub frameworka, np. Springa.

**Przetworzenie logiki aplikacji:** Logika aplikacji (np. zapis do bazy danych, generowanie HTML-a) jest przetwarzana przez komponenty aplikacji (np. kontrolery Spring MVC).

**Zwrot odpowiedzi:** Wynik (np. strona HTML lub JSON) jest zwracany do klienta.

---

***Tomcat w Spring Boot***
Spring Boot całkowicie zmienia podejście dzięki **wbudowanemu Tomcatowi**.

**Wbudowany Tomcat**
Spring Boot dostarcza wbudowaną wersję Tomcata (lub innych serwerów, takich jak Jetty czy Undertow), co pozwala uruchomić aplikację jako samodzielny plik JAR. Nie musisz już tworzyć pliku WAR ani instalować osobnego serwera.

**Proces działania w Spring Boot:**
- Spring Boot uruchamia wbudowany Tomcat podczas startu aplikacji.
- Tomcat nasłuchuje na określonym porcie (domyślnie 8080).
- Spring Boot rejestruje odpowiednie endpointy (np. `/api/users/`) jako serwlety.
- Żądania HTTP są obsługiwane tak samo, jak w klasycznym Springu.

**Korzyści z wbudowanego Tomcata:**
- Brak konieczności konfiguracji zewnętrznego serwera.
- Prostota wdrożenia.
- Szybki czas startu.





