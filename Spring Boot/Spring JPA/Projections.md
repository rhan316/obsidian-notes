Projections w Spring JPA to mechanizm, który pozwala na zwracanie określonych fragmentów danych z zapytań, zamiast całych encji. Dzięki nim możesz precyzyjnie zdefiniować, jakie dane chcesz pobrać z bazy danych, co pozwala na optymalizację zapytań i zmniejszenie ilości przesyłanych danych. Projections umożliwiają zwracanie tylko tych pól, które są naprawdę potrzebne, co szczególnie przydaje się w aplikacjach o dużej skali, gdzie wydajność ma kluczowe znaczenie.

Aby zrozumieć Projections, wyobraź sobie bibliotekę, gdzie każda książka (encja) ma wiele szczególnych informacji, takich jak tytuł, autor, data publikacji, ISBN, liczba stron itp. Jeśli potrzebujesz tylko tytułu i autora, Projections pozwalają poprosić o te dwa konkretne pola zamiast pobierać całą "książkę".

Spring JPA wspiera 3 główne rodzaje Projections:
- Interfejsy (Interface-based Projections).
- Klasy (Class-based Projections).
- Dynamiczne projekcje (Dynamic Projections).
---
***Interface-based Projections***
W tej metodzie tworzysz interfejs, który definiuje gettery dla pól, które chcesz pobrać z bazy danych. Na przykład:
```
... Encja ...
id,
title,
author,
isbn,
pages,
publishedDate
... Encja ...
```
Chcesz zwrócić tylko tytuł i autora książki. Tworzysz interfejs Projection:
```
public interface BookSummary {
	String getTitle();
	String getAuthor();
}

Następnie w repozytorium JPA:
public interface BookRepository extends JpaRepository <Book, Long> {
	List<BookSummary> findBy();
}
```

***Class-based Projections***
W tej metodzie zamiast interfejsu, używasz klasy z konstruktorami, aby reprezentować wynik zapytania.
```
public class BookSummary {
	String title;
	String author;

	public BookSummary(title, author);

	//Gettery, Settery
}

public interface BookRepository extends JpaRepository<Book, Long> {

	@Query("SELECT new com.example.BookSummary(b.title, b.author) FROM Book b)
	List<BookSummary> findBookSummaries();
}
```

***Dynamic Projections***
Dynamiczne projekcje pozwalają na określenie typu projekcji w momencie wywołania metody. Możesz wykorzystywać interfejsy, klasy lub inne podejścia w ramach jednego zapytania.
```
public interface BookTitleOnly {
	String getTitle();
}

public interface BookTitleAndAuthor() {
	String getTitle();
	String getAuthor();
}

public interface BookRepository extends JpaRepository<Book, Long> {
	<T> List<T> findBy(Class<T> type);
}
```