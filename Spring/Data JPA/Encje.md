1. Encja to obiekt Javy odwzorowany na tabelę w bazie danych.
2. @Entity, @Id, @GeneratedValue, @Table, @Column to podstawowe adnotacje.
3. Relację między encjami (np. @OneToMany, @ManyToOne) pozwalają odwzorować relację z bazy danych w modelu obiektowym
4. Operację CRUD na encjach są wykonywane za pomocą repozytoriów Spring Data JPA.

**Relacje między encjami**
- **OneToMany / @ManyToOne -->** Relacja, w której jeden obiekt jest powiązany z wieloma obiektami (np. jeden autor ma wiele wydanych książęk).
- **@OneToOne -->** Relacja jeden-do-jednego (np. jeden użytkownik ma jeden nick).
- **@ManyToMany -->** Relacja wiele-do-wielu (np. wielu studentów jest zapisanych na wiele kursów).

**Cykle życia encji**
1. *New* => Nowa encja, która nie jest jeszcze powiązana z bazą danych.
2. *Managed* => Encja jest zarządzana przez *EntityManager* i odzwierciedla stan w bazie danych.
3. *Detached* => Encja jest zarządzana, ale obecnie nie jest powiązana z kontekstem trwałości.
4. *Removed* => Encja jest oznaczona do usunięcia.

- Encja to obiekt Java, który jest odwzorowaniem (mapowaniem) na tabelę w bazie danych.
- Encja reprezentuje rekordy w tabeli - każda instancja encji odpowiada jednemu wierszowi w tabeli
- Encje są kluczowym elementem w **ORM (Object-Relational Mapping)**, co umożliwia pracę z bazą danych jako obiektami w Javie

**Co to są `@PrePersist` i `@PreUpdate`?** 

Te adnotacje są częścią JPA i oznaczają metody, które powinny zostać automatycznie wykonane przez JPA w określonych momentach.
`@PrePersist` - Metoda z tą adnotacją zostanie wywołana tuż przed zapisaniem nowej encji w bazie danych.
`@PreUpdate` - Metoda z tą adnotacją zostanie wywołana przed aktualizacją istniejącej encji w bazie danych.

`@PrePersist` działa tylko przy pierwszym zapisie, natomiast `@PreUpdate` działa przy każdej aktualizacji encji.