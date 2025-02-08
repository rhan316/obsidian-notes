`equals()` Porównywanie obiektów
Domyślnie w `Object` porównuje referencje `==`
Nadpisujemy go, aby porównał wartości pól.

```
class Person {
 ...

	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true; // Sprawdzanie referencji
		if (obj == null || getClass() != obj.getClass()) return false; // spr. typu
		Person person  = (Person) obj;

		return name.equals(person.name); // Porównanie wartości pola
	}
}
```

---
`hashCode()` Optymalizacja w kolekcjach
Służy do efektywnego wyszukiwania w HashMap, HashSet itp.
Obiekty równe według `equals()` muszą mieć ten sam `hashCode()`

```
@Override
public int hashCode() {
	retunr name != null ? name.hashCode() : 0;
	// Generowanie hashCode na postawie name
}
```
