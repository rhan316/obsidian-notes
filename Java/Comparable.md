`Comparable<T>` w Javie to interfejs, który umożliwia porównywanie obiektów tego samego typu w celu określenia ich kolejności. Jest to przydatne w sytuacjach, gdy chcesz sortować kolekcję obiektów (np. listę) lub w inny sposób porównywać obiekty.

Wyobraź sobie, że masz pudełka z książkami. Chcesz je ułożyć w kolejności alfabetycznej według tytułu. Aby to zrobić, musisz wiedzieć, jak porównać dwa tytuły i stwierdzić, który jest "większy" lub "mniejszy". `Comparable<T>` pozwala Ci definiować takie zasady porównywania.

*Główne cechy interfejsu* `Comparable<T>`
1. **Definicja naturalnego porządku:
   - Klasa implementująca `Comparable<T>` musi dostarczyć logikę porównywania poprzez metodę `compareTo(T t)`.
   - Naturalny porządek to domyślny sposób sortowania obiektów tej klasy.
2. **Jedna metoda do implementacji:**
```
	 int compareTo(T t) => zwraca wartość:
	 1. < 0 jeżeli bieżący obiekt ("ten", czyli `this`) jest mniejszy niż obiekt t
	 2. 0 jeżeli bieżący obiekt jest równy obiektowi t
	 3. > 0 jeśli bieżący obiekt jest większy niż obiekt t

	compareTo(Book other) Integer.compare, aby porównać liczby stron:
	
	Integer.compare(this.pages, other.pages) 
		Zwraca -1, jeśli this.pages < other.pages
		Zwraca 0, jeśli this.pages == other.pages
		Zwraca 1, jeśli this.pages > other pages
```

3. **Przydatny w sortowaniu** - Możesz używać `Comparable` do sortowania obiektów w kolekcjach, takich jak `List`, za pomocą metod takich jak `Collections.sort()` 