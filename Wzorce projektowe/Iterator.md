Wzorzec projektowy *Iterator* jest jednym z klasycznych wzorców. Jego głównym celem jest umożliwienie sekwencyjnego dostępu do elementu kolekcji (np. listy, zbioru, tablicy) bez ujawniania wewnętrznej struktury tej kolekcji.
Wyobraź sobie zestaw kart do gry ułożony w stosie. *Iterator* to ktoś, kto pozwala Ci przejrzeć wszystkie karty jedna po drugiej, bez potrzeby grzebania w stosie lub zmieniania jego układu.

---
**Definicje i składniki wzorca Iterator**

***Iterator (interfejs iteratora)*** Definiuje metody potrzebne do iterowania po kolekcji, taki jak: `hasNext()`: sprawdza czy istnieją kolejne elementy w kolekcji, `next()`: zwraca kolejny element kolekcji i przesuwa wskaźnik. itp.

***Concrete Iterator (konkretna implementacja iteratora)*** Realizuje metody interfejsu iteratora dla konkretnej kolekcji.

***Aggregate (interfejs kolekcji)*** Definiuje metodę `createIterator()`, która zwraca iterator dla danej kolekcji.

***Concrete Aggregate (konkretna kolekcja)*** To implementacja konkretnej kolekcji, która przechowuje dane i potrafi tworzyć iterator.

---
***Jak to działa w praktyce?***
1. *Tworzenie iteratora* - klient *użytkownik wzorca* prosi kolekcję o stworzenie iteratora poprzez metodę `createIterator`.
2. *Iteracja po elementach* - klient używa metod iteratora, takich jak `hasNext`, `next`, aby przejść przez elementy kolekcji jeden po drugim.
3. *Abstrakcja i ukrywanie szczegółów* - klient nie musi wiedzieć, jak dane są przechowywane w kolekcji ani jak działa iteracja w tle. Wystarczy, że zna metody iteratora.

```
// Kolekcja (Concrete Aggregate)
List<String> names = new ArrayList<>();
names.add("Ala");
names.add("Ola");
names.add("Ela");

// Tworzenie iteratora
Iterator<String> iterator = names.iterator();

// Iterowanie po kolekcji
while (iterator.hasNext()) {
	String name = iterator.next();
	print(name);
}
```