To mechanizm umożliwiający przechowywanie danych o stanie użytkownika między kolejnymi żądaniami HTTP. Ponieważ HTTP jest protokołem bezstanowym, sesje pozwalają aplikacjom przechowywać informacje o użytkowniku i jego działaniach w trakcie całej interakcji.

Sesja HTTP to przestrzeń przechowywania danych specyficznych dla użytkownika, którą serwer tworzy na czas trwania interakcji z aplikacją. Przykłady zastosowań: Przechowywanie informacji o logowaniu użytkownika, śledzenie koszyka w sklepie internetowym, zarządzanie danymi formularza między różnymi stronami. Sesje są identyfikowane unikalnym identyfikatorem (np. JSESSIONID), który jest przesyłany między klientem a serwerem, zwykle w ciasteczkach.

---
***Jak działa sesja HTTP?***

**Tworzenie sesji** = Jeśli klient wyśle pierwsze żądanie do serwera, jest tworzona sesja dla tego użytkownika. Serwer generuje unikalny identyfikator sesji i wysyła go klientowi w ciasteczku.

**Zarządzanie danymi sesji** = Serwer przechowuje dane sesji w pamięci, bazie danych lub systemie rozproszonym. Klient przesyła `JSESSIONID` w kolejnych zapytaniach, co pozwala serwerowi przypisać żądanie do istniejącej sesji.

**Kończenie sesji** = Sesja kończy się w przypadku przekroczenia czasu nieaktywności, jawnego zakończenia sesji przez aplikację (np. podczas wylogowania) lub restartu serwera, jeśli sesje nie są utrwalane.

---
Spring Boot automatycznie obsługuje sesje HTTP dzięki integracji z kontenerem serwletów (np. Tomcat, Jetty). Umożliwia to przechowywanie danych specyficznych dla użytkownika sesji.
```
@GetMapping("/set")
public String setSession(HttpSession session) {
	session.setAttribute("user", "Jan Kowalski");
	return "Sesja została ustawiona";
}

@GetMapping("/get")
public String getSession(HttpSession session) {
	String user = (String) session.getAttribute("user");
	return user != null ? "User: " + user : "Brak danych w sesji"
}
```

Domyślny czas trwania sesji zależy od konfiguracji kontenera serwletów. Można ustawić czas trwania sesji w pliku `application.properties`.
`server.servlet.session.timeout=30m`

Spring Boot obsługuje różne sposoby przechowywania sesji.

**Pamięć JVM (domyślna)** Dane sesji są przechowywane w pamięci serwera. Dane sesji są utracone  po restarcie serwera.

**Utrwalanie sesji (Session Persistence)** Przechowywanie sesji w bazie danych, Redis czy innych systemach.

---
**Ważne klasy i interfejsy w Spring**

`HttpSession` Interfejs reprezentujący sesję HTTP. Kluczowe metody to `setAttribute(String name, Object value)` - ustawia atrybut sesji, `getAttribute(String name)`, `invalidate()` - usuwa wszystkie dane z sesji i unieważnia ją.

`SessionRepository` (Spring Session) Interfejs odpowiedzialny za zarządzanie sesjami w zewnętrznych systemach (np. Redis, baza danych).
