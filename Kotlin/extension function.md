To funkcja, która wygląda jak metoda klasy, ale tak naprawdę nią NIE JEST.

Nie modyfikuje klasy.
Nie dotyka jej kodu.
Nie dopisuje magicznych bajtów.

To tylko syntatic sugar - sprytne oszustwo kompilatora.

Np.
```kotlin
fun String.lastChar(): Char {
	return this[this.length - 1]
}
```
I teraz:
```kotlin
println("Hej ty".lastChar())
```
Wygląda jak metoda Stirnga, nie?
Ale Kotlin:
*Nie, spokojnie, to tylko funkcja `lastChar("Hej ty")`, którą zapisałem ładniej.*


### Jak to działa pod spodem?
To:
```kotlin
"tekst".lastChar()
kompilator zmienia na:
lastChar("tekst")
```
Zero magii.
Zero runtime hacków.
Żadnego rozszerzenia klasy jak w C#
Po prostu ładna składnia.

**Sygnatura extension function**
```kotlin
fun <receiverType>.nazwaFunkcji(...)
Receiver to ten typ, po którym możesz wołać funkcję jak metodę.
```
