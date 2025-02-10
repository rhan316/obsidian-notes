## Co to jest Call Stack? 🍉

**Call Stack** (stos wywołań) to struktura danych, którą Java wykorzystuje do zarządzania wywołaniami metod. Każde nowe wywołanie metody jest dodawane do szczytu stosu, a gdy metoda się kończy, jest zdejmowana ze stosu.

## Jak działa Call Stack w Javie? 

Gdy metoda jest wywoływana, Java dodaje nową klatkę (frame) na stos.
Gdy metoda kończy się, klatka jest zdejmowana ze stosu, a sterowanie wraca do poprzedniej metody.
Jeśli stos się przepełni, Java rzuca wyjątek `StackOverflowError`. 
 
**Przykład rekurencyjnej metody:**

```java
public static int factorial(int n) {
	if (n == 1) return 1;
	return n * factorial(n - 1);
}
```

### Call Stack dla `factorial(4)`

| Krok | Wywołanie metody | Call Stack                                                     |
| ---- | ---------------- | -------------------------------------------------------------- |
| 1    | `factorial(4)`   | `factorial(4)`                                                 |
| 2    | `factorial(3)`   | `factorial(3) -> factorial(4)`                                 |
| 3    | `factorial(2)`   | `factorial(2) -> factorial(3) -> factorial(4)`                 |
| 4    | `factorial(1)`   | `factorial(1) -> factorial(2) -> factorial(3) -> factorial(4)` |
| 5    | `return 1`       | `factorial(2) -> factorial(3) -> factorial(4)`                 |
| 6    | `return 2 * 1`   | `factorial(3) -> factorial(4)`                                 |
| 7    | `return 3 * 2`   | `factorial(4)`                                                 |
| 8    | `return 4 * 6`   | `Stos pusty, koniec rekursji`                                  |
