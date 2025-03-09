
**Błędy (Errors) vs. Wyjątki (Exceptions)**
Błędy w Javie dzielimy na dwie główne kategorie:
1. **Errors (Błędy systemowe)** -> Krytyczne problemy na poziomie systemu/JVM, których zazwyczaj nie da się obsłużyć.
2. **Execptions (Wyjątki)** -> Problemy na poziomie aplikacji, które można obsłużyć (np. poprzez `try-catch`).

**Errors (Błędy systemowe)** 
Te błędy zazwyczaj poważnie i wynikają z problemów JVM, np.
- `OutOfMemoryError` - brak pamięci dla aplikacji.
- `StackOverflowError` - przepełnienie stosu (np. nieskończona rekurencja).
- `VirtualMachineError` - poważne błędy JVM, np. awaria maszyny wirtualnej.

**Exceptions (Wyjątki aplikacyjne)**

*Checked Exceptions (Wyjątki sprawdzane)*
Muszą być obsłużone (`try-catch` lub `throws`), inaczej kod nie skompiluje się.
- `IOException` - problemy z operacjami wejścia/wyjścia (np. brak pliku).
- `SQLException` - błędy w bazie danych.
- `ParseException` - błąd parsowania (np. złe formatowanie daty).

*Unchecked Exceptions (Wyjątki niekontrolowane)*
Pochodzą od `RuntimeException`. Nie muszą być obsługiwane, ale mogą powodować awarie programu:
- `NullPointerException` - odwołanie do `null`.
- `IndexOutOfBoundsException` - przekroczenie zakresu tablicy lub listy.
- `ArithmeticException` - np. dzielenie przez zero.
- `IllegalArgumentException` - niewłaściwy argument w metodzie.

