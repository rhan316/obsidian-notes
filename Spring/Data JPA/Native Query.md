Native Query w Spring Data JPA to możliwość wykonywania bezpośrednich zapytań SQL w ramach aplikacji korzystającej z JPA (Java Persistence API). Standardowo, Spring Data JPA wspiera korzystanie z JPQL (Java Persistence Query Language), który jest językiem zapytań specyficznym dla JPA i operuje na encjach zamiast na tabelach baz danych. Jednakże, w niektórych sytuacjach bardziej efektywne lub konieczne może być skorzystanie bezpośrednio z SQL. Wtedy możemy użyć Native Query.

**Kiedy używać Native Query?**
1. Potrzebujesz bardzo specyficznego zapytania, które trudno wyrazić w JPQL (Java Persistence Query Language)
2. Wymagana jest optymalizacja wydajności, np. poprzez użycie specyficznych dla danej bazy danych konstrukcji SQL
3. Masz już istniejące, złożone zapytania SQL, które nie są łatwe do przerobienia na JPQL

```
public interface PersonRepository extends JpaRepository<Person, Long> {

	@Query(value = "SELECT * FROM person WHERE last_name = :lastName", nativeQuery = true)
	List<Person> findByLastNameNative(@Param("lastName") String lastName);
}

 @Query --> adnotacja, która pozwala definiować niestandardowe zapytanie
 value --> tutaj wpisujesz swoje zapytanie SQL
 nativeQuery = true --> mówi Springowi, że zapytanie jest natywnym zapytaniem SQL (a nie JPQL)
 :lastName --> używa się go jako parametru w zapytaniu SQL (@Param("lastName")) służy do podania wartości tego parametru
```

W momencie wywołania metody *findByLastNameNative()*, Spring Data JPA wykona zapytanie, podstawiając wartość parametru przekazanego jako argument metody. Wyniki zapytania są mapowane na encję *Person*.


| Zalety                    | Wady                        |
| ------------------------- | --------------------------- |
| Bezpośredni dostęp do SQL | Niezależność od bazy danych |
| Elastyczność              | Trudniejsze do utrzymania   |
**Adnotacja @Modifying**

*Jeśli chcesz wykonać operację aktualizacji lub usunięcia za pomocą Native Query, musisz użyć adnotacji @Modifying*

```
@Transactional
@Modifying
@Query(value = "...", nativeQuery = true)
void updatePersonFirstName(@Param("id") Long id, @Param("firstName") String firstName);
```

Adnotacja @Modifying informuje Spring Data JPA, że zapytanie nie jest zapytaniem zwracającym wyniki, lecz operacją modyfikacji danych (INSERT, UPDATE, DELETE)