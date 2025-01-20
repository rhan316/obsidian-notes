Od Javy 8 interfejsy mogą zawierać zarówno stałe, jaki i metody statyczne. Są to potężne narzędzia umożliwiające rozszerzenie funkcjonalności interfejsów.

***Stałe w interfejsach***
Wszystkie zamienne zadeklarowane w interfejsie są automatycznie:
1. publiczne `public`
2. statyczne `static`
3. finalne `final`

Oznacza to, że są one stałymi, a ich wartość musi być przypisana w momencie deklaracji. Dostęp do stałych jest możliwy tylko przez nazwę interfejsu.

```
interface Apple {
	String COLOR = "red";
	double WEIGHT = 4.33; 
}

Apple.COLOR => "red";
Apple.WEIGHT => 4.33
```
---

***Metody statyczne w interfejsach***
- Są dostępne tylko przez nazwę interfejsu, nie przez instancję klas
- Mogą zawierać logikę związaną z interfejsem, np. mody pomocnicze lub fabryczne
- Nie mogą być nadpisywane ani dziedziczone przez klasy implementujące interfejs

```
interface MathUtils {
	static int add(int a, int b) {
		return a + b;
	}
	static int multiply(int a, int b) {
		return a * b;
	}

	int sum = MathUtils.add(5, 10); => 15
	int product = MathUtils.multiply(5, 10); => 50
}
```
