### Po co one istnieją?
Żebyś mógł:
- wykonywać operacje NA obiekcie,
- mieć dostęp do jego pól przez `this` albo `it`,
- nie pisać miliona tymczasowych zmiennych
Czyściejszy kod, mniej smrodu więcej elegancji.

### Tabela prawdy

| Funkcja | Receiver | Zwraca      | Użycie                                | Zapamiętaj tak:            |
| ------- | -------- | ----------- | ------------------------------------- | -------------------------- |
| let     | `it`     | wynik bloku | przekształcenia, null-check           | "CHCĘ WARTOŚĆ"             |
| run     | `this`   | wynik bloku | inicjalizacja, kombinowanie           | "ZROBIMY i ZWRÓCIMY"       |
| apply   | `this`   | OBIEKT      | konfiguracja obiektu                  | "USTAWIAM, ZWRACAM OBIEKT" |
| also    | `it`     | OBIEKT      | side effects, debug                   | "A PRZY OKAZJI"            |
| with    | `this`   | wynik bloku | gdy obiekt jest znany, piszesz krócej | "JESTEŚ WEWNĄTRZ OBIEKTU"  |
### LET -> używaj, kiedy chcesz przekształcić obiekt

Najczęściej przy nullach albo mapowaniu.
```kotlin
val len = name?.let { it.length }
```
Tu dostajesz `it`.
***Let = chcę WARTOŚĆ z operacji***

### APPLY -> idealne do konfiguracji obiektu
Piszesz:
```kotlin
val user = User().apply {
	name = "Courtney"
	age = 27
	invisible = true
}
```
Zwraca ten obiekt.
Receiver = `this`
***Apply = "ustawiam i zwracam obiekt"***

### RUN -> robisz coś na obiekcie i zwracasz WYNIK
```kotlin
val result = user.run {
	"$name ma $age lat"
}
```
Zwraca to, co napiszesz jako ostatnią linijkę.
***Run = zrób coś i zwróć wynik***


### ALSO -> jak chcesz odpalić side-effect, ale NIE DOTYKAĆ logiki
Najczęściej debug, walidacje, logi.
```kotlin
val user = User("Courtney")
	.also { println("Tworzę user: $it")}
```

### WITH -> nie jest extension, ale działa jak run
```kotlin
with(user) {
	println(name)
	println(age)
}
```
***With = kod w kontekście obiektu, bez zmiennych tymczasowych***
Najczyściej wygląda, gdy masz dużo operacji na jednym obiekcie.

```ini
apply/also → wracają TO SAMO
run/let   → wracają COŚ INNEGO
apply/run → this
let/also  → it
```

```json
- let — „daj wynik”
    
- apply — „ustawiam obiekt”
    
- run — „robię i zwracam”
    
- also — „robię coś dodatkowego”
    
- with — „wejdź w kontekst i pisz krócej”
```


