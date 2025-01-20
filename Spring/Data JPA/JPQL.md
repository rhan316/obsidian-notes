*JPQL (Java Persistence Query Language* to język zapytań używany w **Java Persistence API (JPA)** do pracy z encjami zamiast bezpośrednio z tabelami w bazie danych.

JPQL jest podobny do SQL, ale operuje na klasach encji i ich polach, a nie na tabelach i kolumnach bazy danych. **Zapytania są bardziej abstrakcyjne i niezależne od *konkretnej* bazy danych**.

*Jak zbudowane są zapytania w JPQL?*
- Klasy i pola zamiast tabel i kolumn. Zamiast operować na tabelach bazy danych, JPQL operuje na klasach encji i ich polach.
- Zapytania JPQL mogą być zbliżone do SQL, ale korzystają z nazw klas oraz atrybutów, co ułatwia manipulowanie(mapowanie) obiektami bezpośrednio.

W Spring Data JPA najczęściej piszesz zapytania JPQL w metodach repozytoriów za pomocą adnotacji *@Query*.
Dzięki JPQL możesz pisać bardziej złożone zapytania, które wykorzystują klasy encji i ich relacje.

W JPQL możesz używać **parametrów nazwanych np. :lastName** lub **indeksowanych (?1, ?2, ...)**. Parametry nazwane są bardziej czytelne i często preferowane. 

**Zalety JPQL**
1. *Abstrakcja od SQL* - nie musisz znać szczegółów konkretnej bazy danych, tylko operujesz na encjach.
2. *Spójność z JPA* - dzięki JPA można łatwo zarządzać relacjami między encjami (np. @OneToMany, @ManyToMany)