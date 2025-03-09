### `throw` - Rzucanie wyjątku

`throw` służy do rzucania wyjątku w danym miejscu kodu.
To jak rzucenie bomby w danym momencie programu - jeśli nie zostanie złapana `try-catch` to program się wywali.
Po `throw` zawsze musi wystąpić instancja wyjątku `new ExceptionType...`
```java
public void sprawdzWiek(int wiek) {
    if (wiek < 18) {
        throw new IllegalArgumentException("Musisz mieć co najmniej 18 lat!");
    }
    System.out.println("Dostęp przyznany.");
}

public static void main(String[] args) {
    sprawdzWiek(16);  // Rzuci wyjątek
}
```
Efekt:
```cpp
Exception in thread "main" java.lang.IllegalArgumentException: Musisz mieć co najmniej 18 lat!
```
Tutaj `throw` wstrzymuje działanie programu i rzuca wyjątek.

### `throws` - Deklaracja wyjątku w metodzie
`throws` informuje, że metoda może rzucić wyjątek, ale go nie obsługuje.
To jak znak ostrzegawczy na drodze: *Uwaga! Ta metoda może wyrzucić wyjątek, przygotuj się na to!*
Stosujemy go w sygnaturze metody, a obsługę przerzucamy na wyższy poziom programu.
