### Czy w ogóle jest `reduce()`?

To jest składanie sekwencji do JEDENJ wartości.
Jak składasz kartkę na pół, potem na pół, potem na pół, aż zostaje jeden gruby kawał.

formalnie:
```json
reduce: a, b, c, d, ... -> wynik
```
Używasz operatora binarnego:
```r
(op): (T, T) -> T
```
Czyli bierzesz DWA elementy, robisz z nich JEDEN...
i powtarzasz...
i powtarzasz...
...
aż zostanie tylko jeden.
Czyli:
```r
(((a op b) op c) op d) ...
```
Jeśli wszystko idzie od lewej.
W równoległym -> cholera wie, różnie -> nie wiadomo 

### 3 wersje `reduce()` - i każda robi coś innego

#### `reduce(BinaryOperator<T> acc)`

Bez identity (bez wartości początkowej).
Zwraca `Optional<T>`.

Użycie:
```java
Optional<Integer> sum = list.stream().reduce((a, b) -> a + b);
```
Strumień pusty -> Optional.empty.


#### `reduce(T identity, BinaryOperator<T> acc)`

Z identity.
Zwraca T, nigdy Optional.
```java
int sum = list.stream().reduce(0, (a, b) -> a + b);
```
Identity = wartość startowa, np.:
- 0 dla sumy
- 1 dla mnożenia
- puste "" dla konkatenacji
- neutralne elementy monoidów (tak, matematyka, przeżyjesz)

### `reducee(identity, acc, combiner)`
Najbardziej popierdolona wersja.
Używana automatycznie przez parallelStream().
Np.
```java
int sum = list.parallelStream()
	.reduce(0,
		(partial, element) -> partial + element, // accumulator
		(left, right) -> left + right    // combiner
	);
```
Tu dzieje się PIEKŁO:
- stream dzieli dane na kawałki,
- każdy kawałek jest redukowany osobno,
- potem łączony combinerem.
Dlatego właśnie operator musi być ASOCJATYWNY.

O tym zaraz.

### Jak działa reduce w praktyce

Wyobraź sobie listę:
```java
[1, 2, 3, 4]
```
Redukcja sekwencyjna
```java
(((1 op 2) op 3) op 4)
```
Redukcja równoległa:
```markdown
   (1 op 2)    (3 op 4)
         \      /
          \    /
           (wynik op wynik)
```
Dowolne kawałki mogą być łączone w dowolnej kolejności.
Więc operator musi to wytrzymać.

### Operator musi być asocjatywny - czyli co?
```java
(a op b) op c == a op (b op c)
```
Np. `+, *, min, max, sumowanie list, łączenie map`
Dlaczego? Bo w parallel stream kolejność łączenia nie jest gwarantowana.

### Największe grzechy użycia `reduce()`

**Robienie nim tego, co można zrobić metodami gotowymi**
```java
zamiast:
	stream.reduce(0, (a, b) -> a + b);
	
rób:
	stream.mapToInt(i -> i).sum();
```
Dobry kod != flexowanie reduce()

**Robienie redukcji na obiektach mutowalnych**
```java
totalne tabu.
	reduce(new ArrayList<>(), (list, e) -> { list.add(e); return list})
```
To jest *zbrodnia*.
Nigdy tak nie rób.
Chcesz zbierać -> używaj `collect()`, nie `reduce()`.

**Używanie nieasocjatywnego operatora**
Odejmowanie w parallel stream?
Gratulacje, właśnie wywołałeś losowość jak RNG w grach.
