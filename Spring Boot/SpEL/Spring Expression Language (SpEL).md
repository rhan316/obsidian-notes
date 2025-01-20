**SpEL** to język wyrażeń używany w Spring Framework, który umożliwia dynamiczne przetwarzanie wartości w aplikacjach Spring. Jest wszechstronnym narzędziem pozwalającym na wykonywanie operacji takich jak: 
- Odczytywanie i ustawianie wartości pól.
- Wywoływanie metod.
- Przetwarzanie tablic, kolekcji i map.
- Obsługa wyrażeń logicznych, matematycznych i warunkowych.
SpEL jest szeroko stosowany w Spring Boot, szczególnie w takich miejscach jak adnotacje, pliki konfiguracyjne czy kontrolery.
---
***Dlaczego warto używać SpEL?***
**SpEL** upraszcza pracę w wielu obszarach Spring, umożliwiając:
1. **Dynamiczne wartości** - Np. w adnotacjach można ustawiać wartości na podstawie logiki.
2. **Łatwą integrację z kontekstem Spring** - SpEL pozwala uzyskiwać dostęp do beanów, parametrów i właściwości konfiguracyjnych.
3. **Zastąpienie kodu Java prostymi wyrażeniami** - możesz przetwarzać dane, unikać powtarzania kodu i poprawiać czytelność.
---
***Podstawowe składniki SpEL***
SpEL korzysta z operatorów, składni i mechanizmów podobnych od innych języków wyrażeń.

**Operatory**

| Nazwa operatoru                             | Opis                       |
| ------------------------------------------- | -------------------------- |
| Logiczne: `and, or, not, !`                 | `true and false` ==> false |
| Porównania: `==, !=, <, >, <=, >=`          | `10 > 5` ==> true          |
| Matematyczne `+, -, *, /, %`                | `10 + 5` ==> 15            |
| Operatory warunkowe: `Ternary ?:, Elvis ?:` | `condition ? 'yes' : 'no'` |

**Dostęp do właściwości**
- Odczyt pola obiektu - `#object.property`
- Wywoływanie metody - `#object.method()`
- Elementy kolekcji i tablic - `list[0]`, `map['key']`

**Wbudowane słowa kluczowe**

`T(ClassName)` Odnosi się do klasy Java.
`T(java.lang.Math).PI` ==> `3.14`

`new` Tworzy nowy obiekt.
`new String('Hello SpEL')` ==> "Hello SpEL".