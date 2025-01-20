Spring MVC (Model-View-Controller) to framework webowy będący częścią ekosystemu **Spring Framework**, używany do budowy aplikacji webowych. Opiera się na architekturze MVC, która oddziela logikę biznesową (Model) od prezentacji (View) i kontroli przepływu (Controller).

---
***Architektura Spring MVC***

Spring MVC opiera się na wzorcu projektowym MVC. Podstawowe komponety:
- **Model** -> reprezentuje dane aplikacji i logię biznesową.
- **View** -> odpowiada za prezentację danych (np. HTML, JSON, XML).
- **Controller** -> obsługuje żądania użytkownika, przetwarza je i przekazuje dane do widoku.

*Przepływ żądania w Spring MVC*
- Klient wysyła żądanie HTTP.
- Żądanie trafia do *DispatcherServlet (Front Controller)*.
- *DispatcherServlet* deleguje żądanie do odpowiedniego **HandlerMapping**, który identyfikuje kontroler.
- Kontroler wykonuje logikę biznesową i zwraca wynik (np. dane w formacie JSON).
- DispatcherServlet przekazuje dane do **ViewResolver**, który renderuje widok (lub bezpośrednio zwraca dane w przypadku API).
- Odpowiedź jest zwracana do klienta.

---
***Kluczowe komponenty Spring MVC***

| NAZWA               | OPIS                                                                                                                                                                                           |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DispatcherServlet` | Główny komponent Spring MVC, działający jako `Front Controller`. Przechowuje wszystkie żądania HTTP i zarządza ich przepływem. Analizuje ścieżki URL, wywołuje kontrolery i zwraca odpowiedzi. |
| `HandlerMapping`    | Mapuje żądania HTTP na odpowiednie metody kontrolera. Przykład `/api/users` może być zmapowane na metodę kontrolera oznaczoną `@GetMapping("/api/users/")`                                     |
| `Controller`        | Komponent, który obsługuje żądania HTTP.                                                                                                                                                       |
| `Model`             | Dane, które aplikacja przetwarza i przesyła między warstwami. Spring MVC udostępnia obiekt `Model` do przekazywania danych z kontrolera do widoku                                              |
| `View`              | Komponent odpowiedzialny za prezentacje danych. Spring MVC obsługuje różne technologie widoku: `JSP`, `Thymeleaf`, `JSON/XML` i inne.                                                          |
| `ViewResolver`      | Komponent odpowiedzialny za wybór odpowiedniego widoku. Mapuje nazwę widoku zwracaną przez kontroler na rzeczywisty plik widoku (np. JSP lub HTML).                                            |

---
## **3. Kluczowe adnotacje Spring MVC**

|**Adnotacja**|**Opis**|
|---|---|
|`@Controller`|Oznacza klasę jako kontroler MVC.|
|`@RestController`|Specjalna wersja `@Controller` zwracająca dane bezpośrednio jako JSON/XML (bez widoku).|
|`@RequestMapping`|Mapuje żądania na metodę lub klasę.|
|`@GetMapping`|Mapuje żądania HTTP GET.|
|`@PostMapping`|Mapuje żądania HTTP POST.|
|`@PutMapping`|Mapuje żądania HTTP PUT.|
|`@DeleteMapping`|Mapuje żądania HTTP DELETE.|
|`@PathVariable`|Pobiera wartości zmiennych z URL (np. `/api/users/{id}`).|
|`@RequestParam`|Pobiera parametry zapytania (np. `?name=John`).|
|`@RequestBody`|Deserializuje ciało żądania (np. JSON) na obiekt Java.|
|`@ResponseBody`|Serializuje obiekt Java na JSON/XML w odpowiedzi HTTP.|
|`@ExceptionHandler`|Obsługuje błędy w obrębie kontrolera.|

---
***Najczęstsze pytania na rozmowach kwalifikacyjnych***

*Czym różni się `@Controller` od `@RestController`?*
`@RestController` to skrót `@Controller` + `@ResponseBody`, co oznacza, że każda metoda zwraca dane w formacie JSON/XML.

*Jak działa DispatcherServlet?*
DispatcherServlet to centralny serwlet w Spring MVC, który zarządza żądaniami HTTP, deleguje je do odpowiednich komponentów i zwraca odpowiedź.

*Jak obsługiwać błędy w Spring MVC?*
Za pomocą `@ExceptionHandler` w kontrolerze lub globalnie za pomocą `@ControllerAdvice`.

*Jak mapować parametry z URL?*
Używając `@PathVariable` (zmienne w ścieżce) lub `@RequestParam` (parametry zapytania).

*Jakie technologie widoku są wspierane przez Spring MVC?*
JSP, Thymeleaf, FreeMaker, JSON, XML.

