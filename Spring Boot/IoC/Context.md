SAC (Spring Application Context) jest centralnym elementem w ekosystemie Spring Framework.
Jest to kontener IoC (Inverion of Control Container), który zarządza całym cyklem życia beanów w aplikacji oraz zapewnia mechanizmy, dzięki którym Twoja aplikacja działa zgodnie z zasadami Springa.
Można go porównać do orkiestry, która zarządza wszystkimi instrumentami (beanami) w Twojej aplikacji, zapewniając, że grają one razem harmonijnie.

---
**Application Context** to zaawansowana wersja **Bean Factory** (bardziej podstawowego kontenera Springa), która oferuje dodatkowe funkcje, takie jak obsługa zdarzeń, międzynarodowe tłumaczenia i integrację z AOP (Aspect-Oriented Programming).
AP:
1. Tworzy, konfiguruje i zarządza obiektami (beanami).
2. Wstrzykuje zależności do tych obiektów.
3. Umożliwia integrację między beanami w aplikacji.
4. Obsługuje rozszerzone funkcje, takie jak zarządzanie zdarzeniami i obsługę właściwości.
---

Jak działa Context Springa?

1. **Rejestracja beanów** - AP rejestruje wszystkie klasy oznaczone jako komponenty `@Component`, `@Service`, `@Repository` lub ręcznie zdefiniowane w plikach konfiguracyjnych.
2. **Tworzenie beanów** - Podczas startu aplikacji Spring tworzy instancje wszystkich beanów i umieszcza je w kontekście. Te instancję są następnie gotowe do użycia.
3. **Wstrzykiwanie zależności** - Context identyfikuje, jakie zależności są wymagane przez każdy bean i wstrzykuje je automatycznie (np. za pomocą `@Autowired`).
4. **Zarządzanie cyklem życia beanów** - Tworzy je podczas startu aplikacji -> wykonuje metody inicjalizujące `@PostConstruct` -> wykonuje metody sprzątające `@PreDestroy` przed zamknięciem aplikacji.
5. **Zdarzenia aplikacyjne** - Context umożliwia publikowanie i nasłuchiwanie zdarzeń, np. `ContextRefreshEvent`, `ContextCloseEvent`.
---
**Typy konteksów w Spring**


| Typ kontekstu                        | Zastosowanie                                                                           | Metody konfiguracji                                   |
| :----------------------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `AnnotationConfigApplicationContext` | Aplikacje skonfigurowane za pomocą adnotacji JavaConfig                                | Konfiguracja z użyciem adnotacji np. `@Configuration` |
| `ClassPathXmlApplicationContext`     | Aplikacje, które wykorzystują pliki XML jako sposób konfiguracji                       | Konfiguracja w pliku XML                              |
| `GenericApplicationContext`          | Uniwersalne podejście do zarządzania różnymi typami konfiguracji (np. XML, Java, itp.) | Programowa lub mieszana konfiguracja                  |
| `WebApplicationContext`              | Aplikacje webowe, które działają w ramach Spring MVC lub innych technologii webowych   | Automatycznie zarządzane przez Springa                |

**AnnotationConfigApplicationContext**
Obsługuje klasy konfiguracyjne oznaczone `@Configuration` - Umożliwia deklarowanie beanów za pomocą metody `@Bean` - Współczesne podejście zalecane w Spring Boot i aplikacjach standardowych

**ClassPathXmlApplicationContext**
Obsługuje konfigurację Springa w plikach XML. Popularne przed wprowadzeniem konfiguracji opartej o Java. Działa o oparciu o schemat XML do definiowania beanów i relacji między nimi

**GenericApplicationContext**
Umożliwia dynamiczne definiowanie beanów i konfiguracji. Nie wymaga sztywnych reguł konfiguracyjnych. Pozwala na konfigurację beanów: `context.registerBean(MyService.class)`

**WebApplicationContext**
Specjalny kontekst dostosowany do aplikacji webowych. Rozszerza funkcjonalność `ApplicationContext` o obsługę serwletów. Tworzony automatycznie w kontenerach webowych (np. Tomcat, Jetty). Współpracuje z kontekstem root `@ContextHierarchy` i kontekstem webowym np. Spring MVC DispatcherServlet.