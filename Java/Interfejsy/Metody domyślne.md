W Javie od wersji 8 wprowadzono możliwość definiowania metod domyślnych (default) w interfejsach. Metody te posiadają domyślną implementację i mogę być wywołane przez klasy implementujące interfejs, jeśli nie nadpiszą ich w swojej własnej implementacji.

***Cechy metod `default` w interfejsach:***
1. **Domyślna implementacja** - Pozwala na dodanie nowej metody do istniejącego interfejsu bez konieczności modyfikowania wszystkich klas, które już ten interfejs implementują.
2. **Opcjonalne nadpisywanie** - Klasy implementujące mogą, ale nie muszą nadpisać metodę `default`
3. **Słowo kluczowe `default`** - Jest wymagane przy deklaracji takiej metody.

```
interface Greeting {
	default String sayHello() {
		return "Hello, there!";
	}
}

class Greeter implements Greeting {
	// Klasa nie musi nadpisywać domyślnej metody, ale może to zrobić
}

class AnotherGreeter implements Greeting {
	@Override
	String sayHello() {
		return "Hi!";
	}
}

psvm {
	var greeter1 = new Greeter();
	greeter1.sayHello(); => "Hello, there!";

	var greeter2 = new AnotherGreeter();
	greeter2.sayHello(); => "Hi!";
}
```