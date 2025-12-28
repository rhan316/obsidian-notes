Interfejs funkcyjny = interfejs dokładnie z jedną metodą abstrakcyjną.

### Co się liczy
- `abstract` -> TAK
- `default` -> NIE
- `static` -> NIE
- `private` -> NIE
- `metody z Object (toString, equals, hashCode)` -> NIE
*Java liczy TYLKO metody abstrakcyjne*.

### Lambda - co robi
```java
Consumer<String> consum = s -> print(s);
```
*Lambda:*
- implementuje interfejs funkcyjny
- nie jest metodą
- nie jest klasą, ale JVM i tak robi z niej obiekt
- implementuje JEDNĄ metodę abstrakcyjną interfejsu

*Mentalny model:*
```java
new Consumer<String>() {
	public void accept(String s) {
		System.out.println(s);
	}
}
```

# `::`
Referencja do metody jest skrótem składniowym do utworzenia *OBIEKTU*, który deleguje wywołanie do wskazanej metody.
```java
Consumer<String> c = sys.out::print;
```
To jest równoważne:
```java
Consumer<String> c = s -> sys.out::print;
```

## ZŁOTA ZASADA `::`

**To NIE metoda wybiera interfejs**.
**To INTERFEJS wybiera metodę.**

- nie niesie typu
- nie zgaduje
- nie wybiera przeciążenia
**Cały sens pochodzi z LEWEJ STRONY `Consumer<String>`.

### Przeciążone metody

Java:
- bierze metodę abstrakcyjną interfejsu
- patrzy na jej sygnaturę
- wybiera JEDNO NAJLEPSZE dopasowanie
```java
Consumer<String> c = System.out::println;
// wybierze println(String)

Consumer<Object> c = System.out::println;
// wybierze println(Object)

// Jeśli nie da się jednocześnie dopasować -> compile-time error
```

## Brak kontekstu = katastrofa
```java
var x = System.out::println; // Wywali od razu Error
```
Dlaczego?
"Nie wiem, kurwa, czego ode mnie chcesz."
Jaki interfejs? Jaka sygnatura?

`::` ZAWSZE potrzebuje:
- interfejsu funkcyjnego
- albo jawnego typu

## Lambda != anonimowa klasa

- lambda nie tworzy nowej klasy (w sensie source-level)
- JVM używa `invokedynamic`
- implementacja może być singletonem, cache'owana, tworzona leniwie.

*Anonimowa klasa:*
- ZAWSZE jest nową klasą
- ma własny `.class`
- ma `this` wskazują na siebie

## `this` w lambdzie != `this` w klasie anonimowej

`this`
- w lambdzie --> `this` = obiekt zewnętrzny
- w anonimowej klasie --> `this` = ta klasa

### Lambda NIE ma własnej tożsamości
`c1.equals(c2); // NIE MA GWARANCJI`
- lambdy nie mają sensownego equals
- nie polegaj na ich tożsamości
- traktuj je jak zachowanie, nie obiekt domenowy

=== aa ===