Adnotacje (ang. annotations) to specjalne konstrukcje w Javie, które umożliwiają dodawanie metadanych do kodu. Metadane te mogą być wykorzystywane prze kompilator lub w czasie wykonywania aplikacji (za pomocą refleksji).

Adnotacje to specyficzne metadane, które dodajesz w kodzie w postaci `@AnnotationName`. Mogą być stosowane do klas, metod, pól, parametrów lub innych elementów.

**Adnotacje są potężnym narzędziem, które pozwala:**
- Upraszczać kod (np. automatyczne mapowanie pól w bibliotekach jak Hibernate).
- Dodawać informacje pomocnicze (np. `@Documented`  generuje dokumentacje).
- Ułatwiać konfigurację (np. `@SpringBootApplication` w Spring Boot). 

Adnotacje definiujemy jak interfejs, ale z użyciem słowa kluczowego `@interface`. Dodatkowo możemy określić, gdzie i jak nasza adnotacja może być stosowana za pomocą dwóch ważnych adnotacji wbudowanych:
- **@Retention** - określa, jak długo adnotacja ma być widoczna.
- **@Target** - określa, do jakich elementów w kodzie można ją stosować.

```
Adnotacja @Task - przechowuje nazwę zadania i jego priorytet

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Task {
	String name(); // Parametr do przechowywania nazwy zadania
	int priority() default 1; // Parametr z domyślną wartością
}
```