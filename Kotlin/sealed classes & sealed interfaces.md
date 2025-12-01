### Po co to w ogóle istnieje?

Bo Kotlin chce, żebyś panował nad hierarchią klas, zamiast pozwalać jej rosnąć jak chwastom.
*sealed* = zamknięte dziedziczenie.

Czyli mówisz:
```
Hej, świat, TYLKO określone klasy mogą po mnie dziedziczyć.
I znam je wszystkie.
```
Brzmi jak kontrola freaka?
Dobrze. W Kotlinie to zaleta.

### sealed class -> klasa zamknięta
```kotlin
sealed class Result
```
Co to znaczy?
- tylko lokalne (w tym samym pliku) klasy mogą po niej dziedziczyć,
- kompilator zna wszystkie możliwe podtypy, więc rozumie, kiedy `when` jest wystarczający i może wymusić, żebyś obsłużył wszystkie przypadki.
Np.
```kotlin
sealed class ApiResponse

data class Success(val data: String): ApiResponse()
data class Error(val msg: String): ApiResponse()
object Loading: ApiResponse()
```

`when` wtedy:
```kotlin
fun handle(response: ApiResponse) = when (response) {
	is Success -> println(response.data)
	is Error -> println("Error: ${response.msg}")
	Loading -> println("Loading...")
}
```
Żadnego `else`
Bo kompilator wie, że nic więcej nie istnieje.

---
## sealed interface - to samo, ale bardziej elastycznie
Od Kotlina 1.5+ możesz mieć `sealed interface Action`
I wtedy:
- klasy implementujące też muszą być w tym samym pliku, chyba że użyjesz sealed + permits w JVM 17 (jest taka furtka, ale to advanced)
- możesz łączyć sealed interface z klasami, które dziedziczą  POZOSTAŁE rzeczy (bo interfejs nie blokuje dziedziczenia tak mocno jak sealed class)
```kotlin
sealed interface Operation


```

