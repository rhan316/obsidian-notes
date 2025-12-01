### `when` to switch na sterydach

W Javie masz switch.
W Kotlinie masz `when`, które jest:
- pełnoprawnym wyrażeniem (może zwracać wartość)
- nie potrzebuje żadnych pojebanych `break`
- działa na typach, przedziałach, warunkach, obiektach
- może być bez else, jeśli przypadki są wyczerpujące
Mądrzejszy, czystszy i mniej debilny niż switch z Javy.

```kotlin
when (x) {
	1 -> print("one")
	2 -> print("two")
	else -> print("something else")
}
```
Zero `break`, zero dramy, Kotlin wie, kiedy kończyć.

### `when` jako wyrażenie (zwraca wartość)
```kotlin
val result = when (x) {
	1 -> print("one")
	2 -> print("two")
	else -> print("something else")
}
```

### Wiele wartości w jednym branchu
```kotlin
when (x) {
	1, 2, 3, 4 -> print("small")
	in 5..10 -> print("medium")
	in 11..100 -> print("big")
	else -> print("large")
}
```

### `when` bez argumentu
Idealne, gdy chcesz testować warunki:
```kotlin
when {
    age == null -> println("brak wieku")
    age < 0 -> println("co to kurwa za wiek")
    age > 150 -> println("nikt tyle nie żyje")
    else -> println("wiek OK")
}
```
Tutaj warunki działają jak `if/else`, tylko czyściej

### `when` + sealed class = magia
Jeśli masz sealed class:
```kotlin
sealed class Response
data class Success(val data: String) : Response()
data class Error(val msg: String) : Response()
object Loading : Response()

To when:

fun handle(r: Response) = when (r) {
    is Success -> println(r.data)
    is Error -> println(r.msg)
    Loading -> println("loading")
}
```
Nie potrzebuje else.
Bo kotlin zna wszystkie podtypy - coś, czego Java może mu pozazdrościć.

### `when` jako zastępstwo dla polimorfizmu (czasem)
```kotlin
fun operation(op: Operation) = when(op) {
	is Add -> op.a + op.b
	is Sub -> op.a - op.b
}
```