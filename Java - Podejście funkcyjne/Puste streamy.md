
### Po co istnieją puste Streamy?

**Bezpieczny "nic-tu-nie-ma" obiekt**
```java
zamiast:
if (list == null || list.isEmpty()) return Stream.empty();

robisz elegancko:
list.stream()
```
A jeśli lista jest pusta -> dostajesz pusty stream, który nie wywali ani nie zrobi ci krzywdy.
To taka... gumowa krawędź na twoim dziecięcym rowerku Java.

Streamy i Lambdy pomagają w czystszych konstrukcjach funkcjonalnych, gdzie operujesz na wartościach, nie na warunkach.

**Zgodność z pipeline'ami**

Stream może być pusty, ale wciąż możesz napisać: `Stream.empty().map(...).filter(...).findFirst();`
i nic nie wybucha.
Wyobraź sobie, że masz potok operacji i nagle musisz przerwać wszystko, bo coś "nie istnieje".
Pusty stream = dobra, jedziemy dalej, nie ma tutaj nic do roboty.

**Unikanie nulli**
Null to gówno.
Pusty stream -> wszystko żyje, nic się nie nulluje.

**Łatwiejsze łączenie źródeł danych**
Chcesz zrobić:
`Stream.concat(streamA, streamB)`
i nie chcesz sprawdzać, czy A albo B przypadkiem nie jest null -> BO CI SIĘ NIE CHCE, oczywiście.
`Stream.empty()` robi robotę.

