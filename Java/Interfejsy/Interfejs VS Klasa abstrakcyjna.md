*Samochód jako klasa abstrakcyjna, a przepisy ruchu drogowego jako interfejs*.

**Klasa abstrakcyjna**
	To blueprint, czyli pewien plan na stworzenie konkretnego samochodu.
	Może zawierać zarówno elementy już gotowe (np. gotową implementację działania silnika), jak i elementy, które pozostawia do uzupełnienia przez konkretne modele samochodów (np. rodzaj napędu - benzynowy, elektryczny, hybrydowy).
	Możesz powiedzieć: "Każdy samochód ma silnik i koła", ale to, jak dokładnie działa silnik i jak działają koła, może się różnić między modelami.
```
	abstract class Car {
	
		// Gotowa część - każdy samochód ma silnik
		void turnOnEngine() {
				... uruchamianie silnika ...
		}

		// Abstrakcyjna część - każdy samochód definiuje swój typ napędu
		abstract void driveType();
	}
```

**Interfejs**
	To bardziej jak lista zasad lub umów, czyli przepisy ruchu drogowego.
	Mówi "Każdy pojazd musi mieć klakson i możliwość zatrzymania się". Ale nie interesuje go jak dokładnie to osiągniesz. Po prostu musisz te metody wdrożyć w swojej klasie.
	Interfejs nie dostarcza nic gotowego - wymaga tylko, żebyś się podporządkował jego zasadom.
```
	interface Vehicle {
		void useHorn();
		void stopVehicle();
	}
```

| Cecha                   | Klasa abstrakcyjna                 | Interfejs                                            |
| ----------------------- | ---------------------------------- | ---------------------------------------------------- |
| Zaimplementowane metody | Tak, mogą być zaimplementowane.    | Tak, od Javy 8 (domyślne, statyczne, prywatne).      |
| Dziedziczenie           | Jedna klasa abstrakcyjna na raz.   | Można implementować wiele interfejsów.               |
| Konstruktor             | Tak.                               | Nie. (interfejsy nie mogą mieć konstruktorów).       |
| Pola                    | Mogą być różnego typu.             | Tylko publiczne, statyczne i finalne.                |
| Hierarchia              | Używana do dziedziczenia zachowań. | Używana do definiowania umiejętności lub kontraktów. |

