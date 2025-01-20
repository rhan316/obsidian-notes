W Javie korzystanie z referencji do interfejsu umożliwia wywołanie metod zdefiniowanych w interfejsie, niezależnie od konkretnej implementacji. To kluczowa praktyka programowania "na interfejsy, a nie na implementacje"

```
interface Animal {
	String makeSound();
}

class Dog implements Animal {
	@Override
	public String makeSound() {
		return "Woof!";
	}

	public void giveBones(int amount) {
		System.out.println("Give a dog + amount + " bones.");
	}
}

class Cat implements Animal {
	@Override
	public String makeSound() {
		return "Meow!";
	}
}

Animal dog = new Dog();
Animal cat = new Cat();

dog.makeSound() => "Woof!"
dog.giveBones() => Błąd! Nie ma dostępu do innych metod niż z interfejsu Animal

cat.makeSound() => "Meow!"
```

***Zalety:***
1. **Elastyczność:** Możliwość zmiany implementacji bez modyfikacji kodu.
2. **Polimorfizm:** Wspieranie różnych implementacji w tym samym kontekście.
3. **Testowanie:** Łatwiejsze tworzenie mocków podczas testów.
4. **Rozdzielenie kontraktu od implementacji:** Interfejs definiuje zestaw metod, a klasy realizują logikę.
