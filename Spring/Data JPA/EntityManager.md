~={12}EntityManager=~ w Spring Framework (i w kontekście JPA - Java Persistence API) to kluczowy interfejs służący do zarządzania encjami w kontekście bazy danych. Jest odpowiedzialny za interakcję między aplikacją a bazą danych, umożliwiając wykonywanie operacji takich jak:
1. **Tworzenie** - zapisywanie nowych obiektów w bazie danych.
2. **Odczyt** - pobieranie danych z bazy danych w postaci obiektów.
3. **Aktualizacja** - modyfikowanie istniejących danych.
4. **Usuwanie** - usuwanie danych z bazy.

**Kluczowe elementy EntityManager**
1. *Zarządzanie cyklem życia encji*:
	- `persist(entity)` - zapisuje nową encję do bazy danych
	- `merge(entity)` - synchronizuje zmiany obiektu z bazą danych
	- `remove(entity)` - usuwa obiekt z bazy danych
	- `find(Class<T>, Object id)` - wyszukuje encję na podstawie jej klucza głównego
2. *Zapytania JPQL i SQL*:
	- `createQuery(String jpql)` - tworzy zapytanie JPQL (Java Persistence Query Language)
	- `createNativeQuery(String sql)` - umożliwia wykonywanie natywnych zapytań SQL
3. *Transakcje*:
	- EntityManager jest zazwyczaj używany w kontekście transakcji, co pozwala na grupowanie wielu operacji w jedną jednostkę pracy
4. *Cache pierwszego poziomu*:
	- EntityManager przechowuje encje w pamięci podczas jednej sesji, co redukuje liczbę zapytań do bazy danych

W Spring Data JPA często nie musimy korzystać bezpośrednio z `EntityManager`, ponieważ dostarcza gotowe interfejsy `(CrudeRepository, JpaRepository)`, które upraszczają interakcję z bazą danych (Spring Data JPA generuje implementacje (klasę) na podstawie interfejsu w czasie kompilacji). Jeśli jednak potrzebujesz bardziej złożonej logiki, możesz bezpośrednio używać `EntityManager`.