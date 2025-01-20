
To interfejs w Spring Data JPA, który jest częścią frameworka Spring Data, pozwalający na realizację zapytań bazujących na przykładowych obiektach *Example*. Dzięki *Query By Example* (QBE) możemy dynamicznie tworzyć zapytania, podając przykład encji jako wzór, który Spring Data JPA, wykorzysta do utworzenia odpowiedniego zapytania.

W QBE zamiast pisać zapytania w JPQL, SQL lub metodach złożonych (findBy), towrzysz przykładowy obiekt, który posiada wypełnione pola, będą kryteriami wyszukiwania.
Mechanizm *QueryByExampleExecutor* w Spring Data JPA analizuje te pola i generuje odpowiednie zapytanie, które następnie wysyła do bazy danych.

Interfejs *QueryByExampleExecutor* zapewnia możliwość używania metod takich jak:
- **findOne(Example < S > example)** --> znajduje pojedyńczy obiekt, który odpowiada podanemu przykładowi
- **findAll(Example < S > example)** --> znajduje wszystkie obiekty, które spełniaja kryteria określone przez przykład
- **findAll(Example < S >, Sort sort)** --> Znajduje wszystkie obiekty zgodnie z przykładem i zwraca je w określonej kolejności
- **count(Example < S > example)** --> zlicza wszystkie obiekty pasujące do przykładu
- **exists(Example < S > example)** --> sprawdza, czy istnieje obiekt pasujący do przykładu

**QueryByExample** opiera się na wykorzystaniu klasy *Example* oraz *ExampleMatcher*. Example reprezentuje przykładową encję, a *ExampleMatcher* pozwala skonfigurować, w jaki sposób dopasowanie powinno działać (np. czy dane mają być dopasowane w sposób rozróżniający wielkość liter).

```
		// Encja
@Entity
public class Person {
	@Id
	private Long id;
	private String firstName;
	private String lastName;
	private Integer age;

	// Getters and Setters
}

// Repozytorium wykorzystujące QueryByExampleExecutor

public interface PersonRepository extends JpaRepository<Person, Long>, QueryByExampleExecutor<Person>

@Service
public class PersonService {
	private final PersonRepository repository;

	public List<Person> findByExample() {
		// Tworzymy przykład obiektu, po którym będziemy szukać
		var person = new Person();
		person.setLastName("Kowalski");

		//Tworzymy Example z naszego przykładu
		Example<Person> example = Example.of(person);

		return repository.findAll(example);
	}
}
```

Aby bardziej precyzyjnie określić, w jaki sposób mają być dopasowane pola - używamy **ExampleMatcher**

```
var matcher = ExampleMatcher.matching()
		.withIngorePaths("age") // ignoruje pole "age"
		.withMatcher("firstName", ExampleMatcher.GenericPropertyMatcher.startsWith()) // dopasowuje imiona zaczynające się od
		.withIgnoreCase(); // ignoruje wielkość liter

var person = new Person();
person.setFirstName("Jan");
person.setLastName("Kowalski");

Example<Person> example = Example.of(Person, matcher);
List<Person> personList = repository.findAll(example);
```

**Zastosowania QueryByExampleExecutor**
- Chcesz szybko prototypować zapytania bez konieczności pisania specjalnych metod czy JPQL
- Potrzebujesz zapytań, które są dynamiczne, zależnie od parametrów wejściowych, ale nie są bardzo złożone
- Chcesz mieć prostą logię wyszukiwania bez nadmiernego skomplikowania kodu repozytorium

!!! Należy pamiętać, że *Query By Example* jest najlepiej używane do prostych zapytań. Gdy potrzebujesz bardziej zaawansowanych kryteriów, warto rozważyć narzędzia takie jak *Specification* lub inne podejścia dostępne w Spring Data JPA