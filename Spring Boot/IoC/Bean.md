W Spring Boot Bean to obiekt, który jest zarządzany przez kontener IoC.
Beany reprezentują podstawowe elementy logiki aplikacji i są automatycznie tworzone, konfigurowane i zarządzane przez Spring na podstawie definicji w kodzie.

---
**Bean** to komponent, który został zarejestrowany w kontenerze Spring, może być automatycznie wstrzykiwany i używany w innych miejscach aplikacji.
**Zarządzanie przez Spring** - Spring decyduje, kiedy bean jest tworzony, inicjowany i niszczony, na podstawie cyklu życia beanów.

---
***Cechy Bean'ów w Spring Boot**

**Zasięgi (Scope)** określają cykl życia beanów.
1. *Singleton (domyślny)* -> jedna instancja beana na cały kontekst aplikacji. Adnotacja `@Scope("singleton")`.
2. *Prototype* -> Nowa instancja beana tworzona przy każdym żądaniu. `@Scope("prototype")`.
3. *Request* -> Jedna instancja na żądanie HTTP.
4. *Session* -> Jedna instancja na sesję HTTP.

---
**Spring zarządza cyklem życia beanów**
1. Tworzenie - Spring tworzy instancję beana.
2. Inicjalizacja - Metody takie jak `@PostConstruct` mogą być używane do inicjalizacji.
3. *Zniszczenie* - Metody oznaczone `@PreDestroy` są wywoływane przed usunięciem beana.