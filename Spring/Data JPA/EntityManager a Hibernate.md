`EntityManager` w kontekście Hibernate jest jednym z kluczowych elementów, ponieważ Hibernate jest najczęściej używaną implementacją *JPA (Java Persistence API)*, a `EntityManager` to interfejs JPA do zarządzania encjami i komunikacji z bazą danych.

1. **Hibernate jako implementacja JPA**
	- JPA to specyfikacja, która definiuje standardowy sposób zarządzania obiektami w relacyjnych bazach danych
	- Hibernate jest implementacją tej specyfikacji dostarczającą wszystkie wymagane mechanizmy, w tym implementację `EntityManager`
2. **EntityManager w Hibernate**
	- W Hibernate `EntityManager` jest abstrakcją nad sesją Hibernate (`Session`), która jest klasą z API Hibernate
	- Gdy używasz Hibernate w aplikacji opartej na JPA, `EntityManager` działa jako wrapper dla `Session`
3. **Hibernate Session vs EntityManager**
	- `Session` to niskopoziomowy interfejs specyficzny dla Hibernate
	- `EntityManager` jest zgodny z JPA i zapewnia bardziej uniwersalne API, niezależnie od konkretnej implementacji (np. Hibernate, EclipseLink)
	- `EntityManager` może być mapowany na `Session`

EntityManager w Hibernate jest abstrakcją JPA nad bardziej specyficznym API Hibernate `Session`.
Używając EntityManager, masz dostęp do standardowego API, które zapewnia przenośność i standaryzację , podczas gdy Hibernate dostarcza konkretną implementację tego interfejsu.
W bardziej zaawansowanych przypadkach możesz użyć `Session` Hibernate, jeśli potrzebujesz funkcji wykraczających poza JPA.