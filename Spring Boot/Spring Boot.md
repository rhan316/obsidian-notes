Spring Boot to narzędzie, które ma na celu uproszczenie korzystania z Spring Framework, dzięki automatyzacji konfiguracji i dostarczeniu gotowych komponentów. Pod maską działa jak potężna maszyna, która wykorzystuje wiele sprytnych mechanizmów, by zaoszczędzić czas programisty i sprawić, że aplikacje działają "od ręki".

*Problem Spring Framework*

Wyobraź sobie, że budujesz domek z klocków LEGO. Spring Framework to zestaw, w którym masz wszystkie klocki do zbudowania dowolnego domu, ale musisz ręcznie dopasowywać każdy element.
- Musisz określić jakie okna chcesz (konfiguracja komponentów).
- Musisz znaleźć odpowiednie drzwi i ustawić je w odpowiednich miejscach (konfiguracja zależności).
- A na końcu upewnić się, że wszystko dobrze współpracuje (sprawdzanie kompatybilności).
To czasochłonne i wymaga wiedzy o każdej części systemu.
---

*Co robi Spring Boot?*

Spring Boot działa jak instruktor, który daje Ci gotowe szablony i mówi "Chcesz dom z jednym piętrem? Mam dla Ciebie gotowy plan. Chcesz dodatkowe piętro? Wystarczy dodać jeden klocek".

**Auto-konfiguracja**
Spring Boot korzysta z mechanizmu auto-konfiguracji `@EnableAutoConfiguration`. Dzięki temu analizuje Twoją aplikację i na podstawie dostępnych bibliotek i zależności, automatycznie dodaje odpowiednie komponenty Spring Framework.
*Jak to działa pod spodem?*
Spring Boot używa klasy `SpringFactoriesLoader`, która ładuje konfiguracje z pliku `META-INF/spring.factories`. W pliku tym znajdują się referencje do klasy konfiguracyjnych, np. klasy odpowiedzialnej za automatyczną konfigurację Hibernate, Tomcat czy JPA.

**Startery**
Spring Boot dostarcza zestaw tzw. **starterów** np. `spring-boot-starter-web` lub `spring-boot-starter-data-jpa`. To nic innego jak predefiniowane zestawy zależności, które są ze sobą kompatybilne i skonfigurowane. Np. `spring-boot-starter-web` zawiera wszystkie narzędzia do budowy aplikacji webowej: Spring MVC, Embedded Tomcat czy Jackson (do serializacji JSON).

**Wbudowane serwery aplikacyjne**
Spring Boot automatycznie dodaje wbudowany serwer aplikacyjny (np. Tomcat, Jetty lub Undertow). Dzięki czemu możesz uruchomić aplikację jako samodzielny proces, bez potrzeby wdrażania jej na zewnętrzny serwer.

---
***Jak działa Auto-konfiguracja krok po kroku?***

Spróbujmy zrozumieć, co się dzieje , gdy uruchamiasz aplikację Spring Boot:
1. **Tworzenie kontekstu aplikacji** - Spring Boot inicjalizuje tzw. **ApplicationContext** - serce Spring, w którym rejestruje wszystkie komponenty i zarządza ich cyklem życia.
2. **Odnajdywanie klasy konfiguracyjnych** - Spring Boot korzysta z adnotacji `@SpringBootApplication`, która jest kombinacją:
	- `@Configuration` - oznacza, że klasa zawiera definicje beanów.
	- `@EnableAutoConfiguration` - włącza mechanizm auto-konfiguracji.
	- `@ComponentScan` - skanuje pakiety w poszukiwaniu komponentów.
3. **Automatyczna rejestracja beanów** - Na podstawie pliku `spring.factories`, Spring Boot sprawdza, jakie klasy powinien załadować jako konfiguracja. Każda taka klasa może rejestrować beany i ustawiać domyślne wartości konfiguracji
4. **Profilowanie i dostosowane** - Spring Boot pozwala na dostosowanie konfiguracji poprzez: pliki `application.properties` lub `appliaction.yml` i profile `spring.profiles.active=dev`, które zmieniają konfigurację w zależności od środowiska.
---

***Najważniejsze mechanizmy Spring Boot pod maską***

**SpringFactoriesLoader** - Główny bohater mechanizmu auto-konfiguracji. Przeszukuje plik `META-INF/spring.factories`, by znaleźć klasy konfiguracyjne.

**Conditional Beans** - Spring Boot korzysta z mechanizmu warunkowego `@Conditional`. Pozwala to ładować beany tylko wtedy, gdy spełnione są określone warunki np.
	`@ConditionalOnClass` - Bean zostaje załadowany, jeśli w classpath znajdzie się określona klasa.
	`@ConditionalOnMissingBean` - Bean zostanie załadowany, jeśli nie istnieje już inny bean tego typu.

**Embedded Server**
Wbudowany serwer (np.Tomcat) działa jak kontener, który nasłuchuje na żądania HTTP i deleguje je do odpowiednich kontrolerów.

---

***Dlaczego Spring Boot jest tak popularny?***

| Powód                                | Opis                                                                                                 |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Mniejsza ilość kodu konfiguracyjnego | Zamiast pisać setki linii XML, wystarczy dodać kilka zależności i Spring Boot zajmuje się resztą.    |
| Szybki start                         | Aplikacje są gotowe do działania od razu po uruchomieniu `java -jar`.                                |
| Łatwe rozszerzanie                   | Jeśli potrzebujesz nowej funkcji, wystarczy dodać odpowiedni starter.                                |
| Wsparcie dla mikroserwisów           | Wbudowane mechanizmy (np. Actuator, Spring Cloud) ułatwiają tworzenie i monitorowanie mikroserwisów. |



