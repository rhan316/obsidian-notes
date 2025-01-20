
| Termin       | Co to jest?          | Rola                                       | Przykład użycia                                 |
| ------------ | -------------------- | ------------------------------------------ | ----------------------------------------------- |
| `collect`    | Metoda na strumieniu | Zbiera elementy strumienia                 | `.collect(Collectors.toList())`                 |
| `Collector`  | Interfejs            | Definiuje strategię zbierania elementów    | Tworzony przez np. `Colectors.toList()`         |
| `Collectors` | Klasa narzędziowa    | Dostarcza gotowe implementacje `Collector` | `Collectors.toMap()`, `Collectors.groupingBy()` |

***`collect` Operacja (metoda)***
To metoda, która jest wywoływana na strumieniu danych (Stream) w Javie. Służy do "zbierania" elementów strumienia i przekształcenia ich w inny format, np. listę, mapę lub coś bardziej złożonego.
*Analogia:* Strumień to taśma produkcyjna, na której przesuwają się różne produkty. Metoda `collect` to końcowy etap, w którym decydujesz, co zrobić z produktami.
```
List<String> names = Stream.of("Alice", "Bob", "Charlie")
	.collect(Collectors.toList());
```


***`Collector` Interfejs (definicja strategii)***
To interfejs, który definiuje, jak elementy strumienia mają być przekształcane. Jest to instrukcja (strategia) mówiąca metodzie `collect`, co dokładnie ma robić.
*Analogia:* Schematy pakowania produktów:
- Jeden schemat pakuje produkty w małe pudełka (lista).
- Inny schemat przypisuje produkty do konkretnych regałów (mapa).
- Jeszcze inny liczy wszystkie produkty.
`Collector` to jak projekt takiego schematu. Mówi on: "Oto jak zebrać produkty z taśmy produkcyjnej".
W powyższym przykładzie użyty jest `Collector` dostarczany przez `Collectors.toList()`. Ten `Collector` określa strategię "Zbierz elementy do listy".

***`Collectors` Klasa narzędziowa (gotowe implementacje Collector)***
To klasa dostarczająca gotowe, fabryczne metody do tworzenia najczęściej używanych `Collector`. Zamiast tworzyć własne implementacje `Collector` (co możesz zrobić), używamy dostarczanych przez `Collectors`.
*Analogia:* Fabryka, gdzie jest gotowy zestaw standardowych pudełek i instrukcji pakowania:
- Pudełko na listy: `Collectors.toList()`.
- Pudełko na mapy: `Collectors.toMap()`.
- Pudełko na zliczenia: `Collectors.counting()`.
Zamiast wymyślać, jak zbudować nowe pudełko, korzystasz z gotowych instrukcji.
```
Map<Integer, String> nameMap = Stream.of("Alice", "Bob", "Charlie")
	.collect(Collectors.toMap(String::length, name -> name));
```