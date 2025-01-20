***Typy opakowujące z cache***
1. `Boolean` - Cache obejmuje wyłączenie dwie wartości: `true` i `false`. Dla każdej operacji, która wymaga opakowania prymitywnego `boolean`, są używane te 2 obiekty.
2. `Character` - Cache obejmuje znaki Unicode w zakresie od 0 do 127.
3. `Short Bye Integer Long` - Cache działa w zakresie od -127 do 127

*Typy bez cache:* `Double` i `Float` - Cache nie istnieje, ponieważ liczby zmiennoprzecinkowe mają ogromną ilość możliwych wartości (część ułamkowa i całkowita), co czyni cache niepraktycznym.

***Inne przypadki, gdzie stosuje się cache w Javie***
1. `String` - Cache działa dla stałych literałów String, dzięki mechanizmowi String Pool. Każdy literał String np. `"Hello"`, jest przechowywany w specjalnej pamięci (String Pool), a ponowne użycie tego samego literału odwołuje się do tego samego obiektu.
2. `Enums` - Obiekty `Enum` są automatycznie przechowywane w pamięci podręcznej. Każda wartość `Enum` jest singletonem w JVM.
3. *Boxing dla prymitywnych typów:* Podczas autoboxingu JVM może stosować cache dla int, short, byte, char, boolean zgodnie z zasadami cache dla typów opakowujących.
4. *Refleksja* - JVM używa cache dla metod, pól i klas uzyskanych przez refleksję, aby przyśpieszyć dostęp do nich podczas wielokrotnego użycia.

***Podsumowanie**
Cache w Javie występuje dla:
1. Typów opakowujących:
	- *Z cache*: Boolean, Character, Byte, Short, Integer, Long.
	- *Bez cache:* Double, Float.
2. String
3. Enum