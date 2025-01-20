
1. Klucz główny (Primary Key)
	1. Primary key to unikalny identyfikator dla każdego wiersza w tabeli. Każda tabela może mieć tylko JEDEN klucz główny, a wartości w tej kolumnie muszą być unikalne i nie mogą być puste (NULL)
	2. Przykład: Kolumna ID w tabeli customers może być kluczem głównym, unikalnie identyfikującym każdego klienta

2. Klucz obcy (Foreign Key)
	1. Kolumna, która tworzy relację między dwiema tabelami. Klucz obcy odnosi się do klucza głównego w innej tabeli, zapewniając spójność danych
	2. Przykład: Kolumna customer_id w tabeli orders jest kluczem obcym, który odnosi się do klucza głównego w tabeli customers, łącząc zamówienia z klientami