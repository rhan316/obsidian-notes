W Javie, Iterable to interfejs, który prezentuje kolekcję, którą można przeglądać element po elemencie. Interfejs ten jest podstawą do działania pętli for-each ( for (type item: collection)), co umożliwia iterowanie po elementach kolekcji w prosty sposób.

```
Iterable jest interfejsem, który zajmuje się w pakiecie java.lang i deklaruje jedną metodę:

public interface Iterable<T> {
	Iterator<T> iterator();
}

Interfejs Iterable wymaga implementacji metody iterator(), który zwraca obiekt typu Iterator. Przykładem klasy implementującej Iterable są klasy kolekcji, takie jak ArrayList, HashSet itp.

List<String> list = new ArrayList<>();
list.add("Java");
list.add("Python");
list.add("JavaScript");

for (String item : list) {
	System.out.println(item);
}
```