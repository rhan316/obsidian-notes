W Javie **ukrywanie implementacji** pole na stosowaniu mechanizmu abstrakcji, które pozwalają użytkownikowi na korzystanie z klasy lub interfejsu bez konieczności znajomości jego wewnętrznej budowy. Osiąga się to poprzez:
1. ~={yellow}Hermetyzację (Encapsulation) =~- ukrywanie pól klasy za pomocą modyfikatora `private` i dostarczanie odpowiednich metod dostępu, ale nie poprzez proste gettery i settery.
2. ~={12}Interfejsy (Interfaces)=~ - definiowanie zachowania, a nie implementacji.
3. ~={9}Dziedziczenie i polimorfizm=~ - używanie abstrakcyjnych klas bazowych.
4. ~={8} Fabryki (Factory Pattern)=~ - tworzenie obiektów bez ujawniania implementacji.
5. ~={10}Modułowość (Modules, Packages)=~ - ograniczenie widoczności klas i metod.