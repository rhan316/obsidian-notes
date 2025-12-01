
### `this` vs `it` - różnica między mówieniem "JA" a "TEN TYP TAM"

#### `this` = ja
Używasz, gdy jesteś wewnątrz obiektu.
Gdy scope function daje ci dostęp do pól, metod, wszystkiego.
Najczęściej pojawia się w:
- `run`
- `apply`
- `with`
Np. `this.name = "Courtney"`
Mówisz: "JA ustawiam swoje pole name"

### `it` = ten jeden, anonimowy obiekt
Używasz, gdy funkcja daje pojedynczy parametr, zazwyczaj nazywany automatycznie jako `it`.
Najczęściej w:
- `let`
- `also`
- lamby, gdzie masz 1 parametr
Np. `it.length`
Mówisz: "Ten obiekt tutaj, co do mnie trafił, jego długość".

## Brutalne podsumowanie

#### `this` -> jestem w środku obiektu, działam jak metoda
```kotlin
run { this. name }
apply { this.age = 20 }
```
Możesz nawet pominąć `this`, bo kontekst jest oczywisty:
```kotlin
apply { name = "Courtney" }
```


#### `it` -> obiekt jest mi PODANY, nie jestem nim
```kotlin
let { it.toUpperCase() }
also { println("Dostałam: $it") }
```

