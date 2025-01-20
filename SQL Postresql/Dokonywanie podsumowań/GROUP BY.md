![[Pasted image 20241024090727.png]]

ZASADY KORZYSTANIA Z **GROUP BY** w POSTGRESQL:
1. Każda kolumna w SELECT, która nie jest używana w funkcji agregującej, musi być obecna w GROUP BY
2. GROUP BY może działać z jedną lub wieloma kolumnami
3. Kiedy korzystasz z GROUP BY, możesz zastosować funkcje agregujące do grupowanych danych , takie jak SUM(), COUNT(), AVG(), MAX(), MIN()
4. Klauzula HAVING działa podobnie do WHERE, ale jest stosowana po grupowaniu. Umożliwia filtrowanie grup na podstawie wyniku funkcji agregujących
5. PostgreSQL nie pozwala używać aliasów zdefiniowanych w SELECT w klauzuli GROUP BY. Musisz odwoływać się bezpośrednio do nazw kolumn.