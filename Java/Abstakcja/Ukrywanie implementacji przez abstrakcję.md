W Javie **ukrywanie implementacji** pole na stosowaniu mechanizmu abstrakcji, które pozwalają użytkownikowi na korzystanie z klasy lub interfejsu bez konieczności znajomości jego wewnętrznej budowy. Osiąga się to poprzez:
1. ~={yellow}Hermetyzację (Encapsulation) =~- ukrywanie pól klasy za pomocą modyfikatora `private` i dostarczanie odpowiednich metod dostępu, ale nie poprzez proste gettery i settery.
2. ~={12}Interfejsy (Interfaces)=~ - definiowanie zachowania, a nie implementacji.
3. ~={9}Dziedziczenie i polimorfizm=~ - używanie abstrakcyjnych klas bazowych.
4. ~={8} Fabryki (Factory Pattern)=~ - tworzenie obiektów bez ujawniania implementacji.
5. ~={10}Modułowość (Modules, Packages)=~ - ograniczenie widoczności klas i metod.
---
#### Hermetyzacja - Ukrywanie pól i operowanie na danych

Zamiast publicznych pól lub prostych getterów i setterów, definiujemy metody operujące na danych.
```java
public class Person {
	private String name;

	public void rename(String newName) {
		if (newName == null || newName.isEmpty()) { throw error };
		this.name = name;
	}

	public String getDisplayName() { return "User: " + name; }
}
name jest prywatne - nie można go bezpośednio modyfikować.
Nie używamy prostego `getName()`, tylko `getDisplayName()`, który może zmienić sposób prezentacji bez zmiany implementacji.
`rename()` sprawdza poprawność danych, zamiast pozwalać na bezpośrednią zmianę name
```

#### Interfejsy - Definiowanie zachowania zamiast implementacji

Interfejs pozwala na określenie co robi klasa, ale nie jak to robi.
`public interface Shape { dobule area(); }`
Teraz różne klasy mogę implementować ten interfejs w sposób, który ukrywa ich szczegóły wewnętrzne.

#### Polimorfizm i klasy abstrakcyjne

Czasami chcemy, aby wszystkie klasy miały pewne wspólne cechy, ale pozostawiamy implementację w rękach dziedziczących.
```java
public abstract class Employee {
	protected String name;

	{ konstruktor }

	public abstract double calculateSalary();
}

Teraz każda klasa dziedziąca musi dostarczyć własną implementację.

public class FullTimeEmployee extends Employee {
	private double monthlySalary;

	public FullTimeEmployee(String name, double monthlySalary) {
		super(name);
		this.salary = salary;
	}
}

```

#### Wzorzec Fabryka (Factory Pattern)
Często chcemy, aby użytkownik nie musiał wiedzieć, jak tworzone są obiekty.
```java
public class ShapeFactory {
	public static Shape createCircle(double radius) { return new Circle(radius); }
	public static Shape createSquare(double side) { return new Square(side); }
}
```