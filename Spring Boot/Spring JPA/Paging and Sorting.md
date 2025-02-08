Wyobraź sobie bibliotekę pełną książek. Chcesz znaleźć konkretną książkę w katalogu, ale zamiast przeglądać całą listę książek, bibliotekarz daje ci kilka stron katalogu z książkami na raz. Na każdej stronie masz ograniczoną liczbę książek - np. 10. Właśnie to jest stronicowanie (Paging).

W kontekście aplikacji:
- *Strona* - to jak kartka w katalogu - zawiera określoną liczbę wyników.
- *Rozmiar strony* - liczba rekordów na jednej stronie (np. 10 książek na stronę).
- *Numer strony* - indeks strony, od której zaczynać przeglądanie (np. strona nr 1).
- *Zastosowanie* - stronicowanie zmniejsza ilość danych przesyłanych między bazą danych a aplikacją, co zwiększa wydajność.

Spring Boot zapewnia obsługę stronicowania za pomocą interfejsu `Pageable`. Możesz określić numer strony i rozmiar strony, a Spring automatycznie wygeneruje odpowiednie zapytanie SQL, aby zwrócić tylko dane z danej strony.


Teraz załóżmy, że chcesz posortować te książki alfabetycznie według tytułu albo według nazwiska autora. Bibliotekarz uporządkowuje je dal ciebie, zanim przekaże katalog. To właśnie jest sortowanie.

W kontekście aplikacji:
- Pole sortowania - kolumna w bazie danych, według której dane mają być posortowane (np. tytuł książki, autor).
- Kierunek sortowania - Czy chcesz sortować rosnąco (A-Z) czy malejąco (Z-A).

Spring Boot realizuje sortowanie za pomocą klasy `Sort`. Możesz połączyć sortowanie z paginacją, aby nie tylko zwracać dane w stronach, ale również w ustalonej kolejności.

---

```
public interface BookRepository extends JpaRepository<Book, Long> {
	Page<Book> findAll(Pageable pageable);
}

... klasa kontrolera ....
	@GetMapping
	public Page<Book> getBooks(
		@RequestParam(defaultValue = "0") int page,
		@RequestParam(defaultValue = "10") int size,
		@ReqestParam(defaultValue = "title,asc") String[] sort
	)

	// Utwórz obiekt Pageable
	var pageable = PageRequest.of(page, size, Sort.of(new Sort.Order.Direction.fromString(sort[1], sort[0])))

	return bookRepository.findAll(pageable);
```

Jak to działa technicznie?

Zapytanie do bazy danych: Gdy Spring Boot otrzymuje żądanie, tłumaczy parametry `Pageable` i `Sort` na odpowiednie zapytanie SQL, np.
`SELECT * FROM books ORDER BY title ASC LIMIT 10 OFFSET 0`

`LIMIT 10` -> pobierz maksymalnie 10 rekordów.
`OFFSET 0` -> zacznij od pierwszego rekordu (dla strony 0).

Spring Boot zwraca dane w obiekcie `Page` zawierającym listę wyników i informacje o bieżącej stronie, liczbie wszystkich stron, liczbie rekordów itp.

---
