**System** to klasa wbudowana w Javę, która znajduje się w pakiecie `java.lang`. Jest to klasa narzędziowa, co oznacza, że udostępnia zestaw statycznych metod i pól, które programista może wykorzystać bez potrzeby tworzenia instancji tej klasy (czyli bez potrzeby pisania `new System()`).
Można porównać klasę `System` do centralnej konsoli w domu, która pozwala:
- Sprawdzić aktualny czas, np. `System.currentTimeMillis()`.
- Wysłać wiadomość przez mikrofon, np. `System.out.print()`.
- Odebrać wiadomości, np. `System.in` do wprowadzania danych z klawiatury.
- Wykonywać inne operacje systemowe, takie jak ustawianie właściwości środowiska.

---
**System.out**
`System.out` to statyczne pole klasy `System`, które reprezentuje standardowe wyjście (domyślnie konsola). Jest to instancja klasy `PrintStream`. Gdy piszesz `System.out.print()`, tak naprawdę używasz metody `print()` klasy `PrintStream`. To jak megafon podłączony do konsoli - wszystko, co "mówisz", pojawia się na ekranie.

**System.in**
Statyczne pole klasy `System`, które reprezentuje standardowe wejście (domyślnie klawiatura).
Instancja klasy `InputStream`. Służy do odczytywania danych wejściowych od użytkownika.

**System.err**
Standardowy strumień błędów. Domyślnie działa jak System.out, ale jest używany specjalnie do wypisywania komunikatów o błędach. Jest to instancja klasy `PrintStream`, ale używana do oddzielenia błędów od standardowego wyjścia.

---
Klasa `System` działa jako pośrednik pomiędzy użytkownikiem a systemem operacyjnym w kontekście wejścia/wyjścia. Jednak sama klasa `System` nie implementuje bezpośrednio żadnej logiki obsługi danych. Zamiast tego odwołuje się do mechanizmów niskopoziomowym z pakietów IO i NIO.