Wszystkie obiekty zarządzane przez Spring'a to tzw. beany. Spring identyfikuje beany na podstawie: adnotacji takich jak `@Component`, `@Service`, `@Repository`, definicji w pliku konfiguracyjnym XML (stare podejście), definicji w klasach konfiguracyjnych z `@Configuration`.

```
@Component
public class BookDTO {
	// ciało klasy
}
```

Adnotacja `@Autowired` mówi Springowi: "Wstrzyknij mi odpowiedni obiekt tutaj". Szuka odpowiedniego beana w swoim kontenerze IoC na podstawie typu klasy.
```
public class MyService {
	private final MyRepository repo;

	@Autowired
	public MyService(MyRepository repo) {
		this.repo = repo;
	}
}
```
W wersjach Springa od 4.3 wprowadzono możliwość automatycznego wstrzykiwania zależności do konstruktorów w przypadku,~={9} gdy klasa ma tylko jeden konstruktor.=~ Konstruktor jest naturalnym miejscem przekazywania zależności. Automatyczne wstrzykiwanie zmniejsza ilość "szumu" w kodzie. Deweloperzy nie muszą pamiętać o dodaniu adnotacji, co zmniejsza ryzyko pomyłek.

Możesz zdefiniować wiele implementacji tej samej zależności i używać adnotacji `@Qualifier`, aby wskazać konkretną implementację.
```
@Component
@Qualifier("myCustomRepo")
public class CustomBookRepo implements BookRepo {
	// specjalna implementacja
}
```

**Jak proces wstrzykiwania zależności działa pod maską?**

Podczas startu aplikacji Spring Boot (np. za pomocą klasy z `@SpringBootApplication`), Spring inicjalizuje swój kontener IoC.
Spring skanuje w poszukiwaniu klas oznaczonych adnotacji, np. `@Component`.
Dla każdej znalezionej klasy Spring tworzy obiekt (bean) i zapisuje go w kontenerze.
Gdy Spring napotka `@Autowired`, `@Inject` lub inny sposób deklarowania zależności:
1. Sprawdza, czy w kontenerze IoC znajduje się pasujący bean.
2. Jeśli jest, wstrzykuje go.
3. Jeśli nie ma, zgłasza wyjątek, np. `NoSuchBeanDefinitionExpection`.

---
**Zalety takiego podejścia**

*Luźne powiązanie (loose coupling)* - Klasy nie są odpowiedzialne za tworzenie swoich zależności. Dzięki czemu są bardziej elastyczne i łatwiejsze w testowaniu.
*Łatwość testowania* - Możesz łatwo podmienić zależności na fałszywe obiekty (mocki) w testach.
*Modularność* - Możesz łatwo wymieniać komponenty (np. różne implementacje interfejsu).

---
**Konflikty w beanach**

Spring radzi sobie z konfliktami między różnymi beanami poprzez mechanizmy identyfikacji i kwalifikacji beanów. Konflikty mogą wystąpić, gdy w kontenerze IoC Spring znajduje więcej niż jeden bean tego samego typu lub Spring nie jest w stanie jednoznacznie określić, który bean powinien zostać wstrzyknięty w danym miejscu.

```
@Component
public class ServiceA {
 ...	Repo repo;

	public ServiceA(Repo repo) {
		this.repo = repo;
	}
}

@Component("repo1")
public class RepoA implements Repository { // implementacja}

@Component("repo2")
public class RepoA implements Repository { // implementacja}

W tym przypadku ServiceA wymaga obiektu typu Repo.
Spring znajdzie dwa beany (repo1 i repo2), ale nie będzie wiedział, który z nich wstrzyknąć.
```

Jeśli Spring nie może jednoznacznie określić, który bean użyć zgłasza wyjątek:
`NoUniqueBeanDefinitionException: No qualifying bean of type 'Repository' available: expected single matching bean but found 2: repo1,repo2
`
**Jak rozwiązać konflikt między beanami?**

~={red}A.=~ Spring nadaje domyślną nazwę każdemu bean'owi na podstawie nazwy klasy (z małą literą) lub nazwy zdefiniowanej w adnotacji, np. `@Component("repo1")`.
Rozwiązanie: ~={green}*Wstrzykiwanie po nazwie bean'a*=~- możesz użyć adnotacji `@Qualifier` lub nazwy parametru konstruktora.
```
@Qualifier("repo1")
private final Repo repo;
```


~={red}B.=~ Możesz oznaczyć jeden bean jako domyślny za pomocą `@Primary`.
```
@Component
@Primary
public class ClassA implements Repo {}

@Component
public class ClassB implements Repo {}
```
Spring wybierze `ClassA` jako domyślny bean, jeśli `@Qualifier` nie zostanie użyty.


~={red}C.=~ Możesz używać różnych beanów w zależności od środowiska (np. dev, test, prod) za pomocą `@Profile`.
```
@Component
@Profile("dev")
public class DevRepo impl Repo {}

@Component
@Profile("prod")
public class ProdRepo impl Repo {}
```
Spring aktywuje tylko te beany, które pasują do aktywnego profilu.

~={red}D. =~ Zamiast adnotacji `@Component`, możesz definiować beany ręcznie w klasie konfiguracyjnej.
```
@Configuration
public class AppConfig {

	@Bean
	public Repo repoA {
		return new RepoA();
	}

	@Bean
	public Repo repoB {
		return new RepoB();
	}
}
```

***Rozszerzone mechanizmy rozwiązywania konfliktów***

~={magenta}A. =~Lista lub mapa beanów `@Autowired Collection/Map`.
Jeśli potrzebujesz wszystkich implementacji danego interfejsu, możesz zażądać jako listy lub mapy.
```
@Autowired
private List<Repository> repoList; // Wszystkie beany typu Repos

@Autowired
private Map<String, Repo> repoMap; // Nazwa beana jako klucz
```
Spring automatycznie zbierze wszystkie beany typu `Repo` i wstrzyknie je do listy lub mapy.

~={magenta}B.=~ Użyj `@Conditional`, aby włączyć lub wyłączyć bean w zależności od określonych warunków.
```
@Component
@Conditional(MyCustomCondition.class)
public class RepoA impl Repo {}
```
Bean zostanie włączony tylko wtedy, gdy warunek zdefiniowany w `MyCustomCondition` zostanie spełniony. 


C. Możesz zdefiniować własne kwalifikatory, aby odróżniać beany:
```
@Target({ElementType.FILED, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface CustomQualifier {
	String value();
}
```

