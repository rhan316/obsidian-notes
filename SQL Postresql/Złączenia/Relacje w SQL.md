1. Wiele do Jednego (Many-to-One)
	1. Każdy wiersz w tabeli A może odnosić się do wielu wierszy w tabeli B, ale każdy wiersz w tabeli B ma co najwyżej jeden odpowiadający mu wiersz w tabeli A.
	2. Przykład: W tabeli orders wiele zamówień może odnosić się do jednego klienta (customer_id jako klucz obcy)

2. Jeden do Wielu (One-to-Many)
	1. Jest to odwrotność relacji wiele do jednego
	2. Każdy wiersz w tabeli A może mieć wiele odpowiadających mu wierszy w tabeli B
	3. Przykład: Każdy klient z tabeli customers może mieć wiele zamówień w tabeli orders

3. Jeden do Jednego (One-to-One)
	1. Każdy wiersz w tabeli A ma dokładnie jeden odpowiadający mu wiersz w tabeli B i odwrotnie.
	2. Przykład: Tabela users może mieć tabelę user_profiles, gdzie każdemu jednemu użytkownikowi odpowiada jeden profil. Klucz podstawowy jednej tabeli jest kluczem obcym w drugiej

4. Wiele do Wielu (Many-to-Many)
	1. Każdy wiersz w tabeli A może być powiązany z wieloma wierszami w tabeli B, a każdy wiersz w tabeli B może być powiązany z wieloma wierszami w tabeli A.
	2. Do implementacji tej relacji potrzebna jest relacja pośrednia (łączna)
	3. Przykład: W tabelach students i courses, każdy student może być zapisany na wiele kursów, a każdy może mieć wielu studentów. Tworzy się tabelę pośrednią enrollments, która przechowuje informację o zapisach