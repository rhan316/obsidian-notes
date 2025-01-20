Criteria API w Javie to część specyfikacji JPA (Java Persistence API), która umożliwia programistom tworzenie dynamicznych i typowanych zapytań do bazy danych w sposób programistyczny.
Jest to alternatywa dla JPQL (Java Persistence Query Language), gdzie zapytania są tworzone jako ciągi znaków (String).

**Główne zalety Criteria API**
1. **Dynamiczność** - Można łatwo tworzyć zapytania w oparciu o warunki, które nie są znane w momencie kompilacji.
2. **Typowanie** - Dzięki wykorzystaniu API typowanego (type safe), błędy są wykrywane już na etapie kompilacji.
3. **Łatwiejsze refaktoryzowanie**  - Przy zmianie nazw pól w encjach IDE może automatycznie dostosować zapytania.
4. **Unikanie błędów literówek** - Dzięki oparciu o klasy i metody zamiast stringów

```
@Entity
public class Person {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private String name;
	private int age;

	// Gettery i settery
}

public class CriteriaExample {
		pvsm {
			var emf = Persistence.createEntityManagerFactory("myEntity");
			var em = emf.createEntityManager();

			try {
				// Rozpoczynamy transakcję
				em.getTransaction.begin();

				// Tworzymy CriteriaBuilder
				var cb = em.getCriteriaBuilder();

				// Tworzymy CriteriaQuery
				CriteriaQuery<Person> cq = cb.from(Person.class);

				// Określamy korzeń zapytania (encja)
				Root<Person> person = cq.from(Person.class);

				// Dodajemy warunek (np. osoby starsze niż 25 lat)
				cq.select(person).where(cb.gt(person.get("age"), 25));

				// Tworzymy zapytanie typu TypedQuery
				TypedQuery<Person> query = em.createQuery(cq);

				// Wykonujemy zapytanie i pobieramy wynik
				List<Person> results = query.getResultList();

				// Wykonujemy zapytanie i pobieramy wynik
							results.forEach(p -> System.out.println(p.getName() + " - " +  p.getAge()));

				// Zakończ transakcję
				em.getTransaction().commit();
			}
	}
}
```

**Elementy składowe Criteria API**
- **CriteriaBuilder** - główny interfejs do tworzenia zapytań i warunków
- **CriteriaQuery** - reprezentuje zapytanie
- **Root** - punkt startowy zapytania (reprezentuje encję)
- **Predicate** - reprezentuje warunki zapytania
- **TypedQuery** - służy do wykonania zapytania