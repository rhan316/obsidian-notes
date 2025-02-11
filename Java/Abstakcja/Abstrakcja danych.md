#### Dlaczego warto używać zmiennych prywatnych?

Główna idea: Zmienność i swoboda zmian - ukrywamy implementację, aby w przyszłości móc modyfikować sposób przechowywania danych bez wpływu na kod zewnętrzny.
Częsty błąd: Automatyczne dodawanie getterów i setterów, które ujawniają implementację i niwelują korzyści wynikające z prywatnych danych.

---
#### Różnice między danymi konkretnymi a abstrakcyjnymi

```java
// Dane konkretne - bezpośrredni dostęp do pól np.
public class Point {
	public double x;
	public double y;
}
Użytkownik wie, jak są przechowywane dane (współrzędne prostokątne).
Brak elastyczności w przyszłych zmianach implementacji.
```
**Dane abstrakcyjne** - dostęp przez metody
```java
public interface Point {
	double getX();
	double getY();
	void setCartesian(double x, double y);
	double getR();
	double getTheta();
	void setPolar(double r, double theta);
}
Użytkownik nie wie, czy dane są przechowywane jako współrzędne prostokątne czy biegunowe.
Możliwość zmiany implementacji bez wpływu na użytkowników.
```

---
#### Abstrakcyjna reprezentacja danych
```java
Przykład pojazdu konkretnego:
public interface Vehice {
	double getFuelTankCapacityInGallons();
	double getGallonsOfGasoline();

	Użytkownik zna szczegóły implementacyjne (galony paliwa)
}

Przykład pojazdu abstrakcyjnego:
public interface Vehile {
	double getPercentFuelRemaining();

	Użytkownik nie wie, czy wartości pochodzą z galonów, litrów czy innej jednostki
}

```
**Powinniśmy opisywać dane w sposób abstrakcyjny, a nie udostępniać szczegółów implementacji.**

---
#### Antysymetria danych i obiektów

- Struktury danych np. `Square, Rectangle, Circle` - udostępniają dane, ale nie mają logiki.
- Obiekty - ukrywają dane i udostępniają operacje na nich.

```java
Przykład proceduralny (z danymi konkretnymi)

Klasy przechowują dane, a operacje są w osobnej klasie `Geometry`:
public class Geometry {
	public double area(Object shape) {
		if (shape instanceof Square) { ... }
		else if (shape instanceof Rectangle) { ... }
		else if (shape instanceof Circle) { ... }
	}

	Łatwo dodać nowe operacje (np. perimeter())
	Trudno dodać nowy kształt (trzeba zmienić wszystkie operacje w Geometry)
}


Przykład obiektowy (z abstrakcją)

Każdy kształt posiada własną metodę `area()`
public class Circle implements Shape {
	public double area() { return Math.PI * radius * radius; }
}

```
**Kod proceduralny** - łatwiej dodawać operacje, trudniej nowe typy danych.
**Kod obiektowy** - łatwiej dodawać nowe typy danych, trudniej nowe operacje.


### Podsumowanie
1. Nie używaj getterów i setterów bezmyślnie - to tylko pozory hermetyzacji.
2. Ukrywaj implementacje przez abstrakcję, a nie dodatkową warstwę metod.
3. Kod proceduralny - ułatwia dodawanie nowych funkcji, ale utrudnia dodanie nowych typów danych.
4. Kod obiektowy - ułatwia dodawanie nowych typów danych, ale utrudnia dodanie nowych funkcji.
5. Prawo Demeter - nie "przechodź" przez zbyt wiele obiektów.
6. Unikaj hybryd - mieszanie obiektów i struktur danych prowadzi do słabej architektury.
7. DTO i Active Record to struktury danych, a nie obiekty biznesowe