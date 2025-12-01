Kotlin nienawidzi NULLi.
Kotlin mówi: "Nie, kurwa, nie pozwolę ci zrobić takiego bałaganu."

Dlatego masz dwa typy:

### Typy nie-nullowalne
`Int, String, User` cokolwiek.
Nie mogą być null. Nigdy.

### Typy nullable (z `?`)
`Int?, String?, User?`
Mogą być null... ale wtedy musisz to przyznać jak dorosły.

## Operatory, czyli narzędzia do ujarzmiania burdelu

### `?.` - bezpieczne wywołanie
Wykonaj, ale jak będzie null, to po prostu daj null, nie dramatyzuj.
`val len = name?.length`
Bezpieczne. Grzeczne. Nie wybuchnie.

### `?:` - operator elvisa
Jak jest null -> weź to, co masz po prawej.
`val age = inputAge ?: 0`
W skrócie: "null? pierdol się, biorę default 0"

## `!!` - nie rób tego, błagam
Wiem, lepiej. Obiecuję, że tu nie będzie null... chyba.
```kotlin
val name = user!!.name
```
Jeśli jednak będzie null -> BOOM! -> NPE.
To jest jak odbezpieczenie granatu i liczenie na szczęście.

## `let { }` - null tylko jeśli naprawdę null
Używasz, gdy chcesz wykonać blok TYLKO jeśli wartość nie jest nullem.
`email?.let { sendEmail(it) }`
Czyli: Jak istniejesz, to chodź tu. Jak nie - fuck off.

