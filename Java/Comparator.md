`Comparator<T>` w Javie to interfejs, który umożliwia definiowanie niestandardowych zasad sortowania dla obiektów. W przeciwieństwie do `Comparable<T>`, gdzie naturalny porządek sortowania jest definiowany w samej klasie, `Comparator` pozwala tworzyć różne sposoby sortowania bez zmiany oryginalnej definicji klasy.

*Podstawowe cechy `Comparator<T>`
1. **Oddzielna klasa** -> `Comparator<T>` jest niezależny od klasy obiektu, który ma być sortowany. Możesz mieć wiele różnych `Comparatorów` dla jednej klasy
2. **Metoda do implementacji** -> `int compare(T o1, T o2)`
3. **Wiele porządków** -> Możesz stworzyć różne sposoby sortowania obiektów tej samej klasy, np. według różnych pól

Zamiast tworzyć osobne klasy dla każdego `Comparator`, możesz użyć lambd do zdefiniowania logiki porównywania bezpośrednio.

```
List<Person> people = new ArrayList<>();

// Sortowanie według wieku
people.sort((p1, p2) -> Integer.compare(p1.getAge(), p2.getAge()));

// Sortowanie według imienia
people.sort((p1, p2) -> p1.getName().compareTo(p2.getName()));


// Jeszcze bardziej uproszczona definicja Comparator, dzięki metodom statycznym
people.sort(Comparator.comparing(Person::getAge()));
people.sort(Comparator.comparing(Person::getName));

```

***Zaawansowane możliwości `Comparator<T>`***

**Odwracanie porządku (`reversed()`)**
	Odwraca kolejność sortowania -> `people.sort(Comparator.comparing(Person::getAge).reversed());`

**Łączenie wielu kryteriów `thenComparing`**
	Pozwala na sortowanie według kilku pól
`people.sort(Comparator.comparing(Person::getAge).thenComparing(Person::getName)`

**Obsługa wartości null (nullsFirst, nullsLast)**
	Możesz określić, czy wartości `null` mają być na początku czy na końcu
	`people.sort(Comparator.comparing(Person::getName, Comparator.nullsFirst(String::compareTo)`