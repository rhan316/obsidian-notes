Typ pierwszo klasowy - funkcje mogą być traktowane jako dane, więc mogą być przekazywane jako argumenty, zwracane przez inne funkcje i przypisywane do zmiennych

Funkcja wyższego rzędu - funkcje, które mogą przyjmować inne funkcje jako argumenty lub zwracać funkcję jako wyniki. Dzięki wyrażeniom lambda i interfejsom funkcyjnym, Java obsługuje funkcje wyższego rzędu, co umożliwia bardziej złożone i elastyczne konstrukcje programistyczne.

```
Przykład funkcji jako typu pierwszo klasowego:

Function<Integer, Integer> powerTwo = x -> x * 2;
int result = powerTwo.apply(5); // 10
```
```
public int applyFunction(Function<Integer, Integer) fun, int wartość) {
	return fun.apply(wartość)
}
```

Kompozycja funkcyjna

To technika polegająca na łączeniu dwóch lub więcej funkcji, tak aby wynik jednej funkcji stał się argumentem kolejnej. W Javie jest to możliwe dzięki wyrażeniom lambda i interfejsom funkcyjnym.
```
Function<Integer, Integer> addSix = a -> a + 6;  
Function<Integer, Integer> divTwo = d -> d / 2;  
Function<Integer, Integer> multiThree = m -> m * 3;  

Jeśli int value = fullCalc.apply(12)

Function<Integer, Integer> fullCalc = addSix // 12 + 6 = 18  
.andThen(divTwo) // 18 / 2 = 9
.andThen(multiThree); // 9 * 3 = 27
```