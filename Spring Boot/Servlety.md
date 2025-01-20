Sewlety to klasy Java obsługujące żądania HTTP w aplikacjach webowych. Są odpowiedzialne za przetwarzanie żądań od klientów (np. przeglądarek) i generowanie odpowiedzi. Servlet API jest częścią specyfikacji **Jakarta EE**.
Servlety to fundament technologii **Java EE (Jakarta EE)** i są kluczowym elementem w zrozumieniu, jak działa Spring/Spring Boot w kontekście aplikacji webowych. Spring Boot wprowadza abstrakcję nad serwletami, ale wiedza o nich jest wciąż ważna.

---

***Kluczowe klasy i interfejsy w Servlet API***

| Nazwa             | Opis                                                         | Ważne metody                                                                                                                                                             |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `HttpServlet`     | Główna klasa bazowa dla serwletów obsługujących HTTP.        | `doGet()`- Obsługuje żądania HTTP GET. `doPost()` - HTTP POST. `doPut()`, `doDelete()`                                                                                   |
| `ServletRequest`  | Reprezentuje żądanie HTTP.                                   | `getParameter(String name)`: pobiera parametr z zapytania. `getAttribute(String name)`: Pobiera atrybut żądania. `getInputStream()`: Pobiera strumień danych wejściowych |
| `ServletResponse` | Reprezentuje odpowiedź HTTP.                                 | `getWriter()` : Pobiera obiekt do zapisu treści odpowiedzi. `setContentType(String type)`: Ustawia typ odpowiedzi (np. text/html)                                        |
| `ServletConfig`   | Przechowuje konfigurację serwletu                            | `getInitParameter(String name)`: Pobiera parametry inicjalizujące serwletu                                                                                               |
| `ServletContext`  | Umożliwia współdzielenie danych między serwletami aplikacji. | `getAttribute(String name)`: Pobiera atrybut współdzielony. `getResourceAsStream(String path)`: Pobiera zasoby (np. pliki)                                               |

---
***Cykl życia serwletu***

Serwlet ma jasno zdefiniowany cykl życia.
**Inicjalizacja (`init()`)** - Wywoływane raz po załadowaniu serwletu. Można w nim przygotować zasoby, np. nawiązywać połączenie z bazą danych. 

**Przetwarzanie żądań (`service()`)** - Wywoływane dla każdego żądania. Domyślnie deleguje obsługę do metod takich jak `doGet()` czy `doPost()`.

**Zniszczenie (`destroy()`)** - Wywoływane przed usunięciem serwletu z pamięci. Służy do zwolnienia zasobów.

---

***Servlety w Spring Boot***
Spring Boot używa serwletów w tle, ale większość pracy wykonują kontrolery i komponenty Spring MVC.
- Wbudowany serwer (Embedded Servlet Container) - Spring Boot dostarcza wbudowany serwer (np. Tomcat, Jetty), który obsługuje servlety. Serwlety są rejestrowane automatycznie.
- Definiowanie własnych serwletów.
```
	@Configuration 
	public class ServletConfig { 
		@Bean 
		public ServletRegistrationBean<MyServlet> myServlet() { 
			return new ServletRegistrationBean<>(new MyServlet(), "/my-servlet"); } }
```
- Spring MVC jako abstrakcja nad servletami - `@Controller, @RestController` to abstrakcje nad servletami. Spring zarządza cyklem życia obiektów, mapowanie URL, serializacją danych.

---
**Przykładowe pytania**
1. Co to jest serwlet i jakie ma zastosowanie?
2. Jak działa cykl życia serwletu?
3. Jakie są kluczowe różnice między `doGet()` a `doPost()`?
4. Co to jest `ServletConfig` i `ServletContext`?
5. Jak Spring Boot obsługuje serwlety w wbudowanym serwerze Tomcat?
6. Jak zarejestrować własny serwlet w aplikacji?