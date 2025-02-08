Wzorzec projektowy **Prototype** to jeden z wzorców kreacyjnych.
Służy do tworzenia nowych obiektów poprzez kopiowanie już istniejących, zamiast inicjalizowania ich od zera. Pomaga to w uniknięciu kosztownej inicjalizacji obiektów oraz zwiększa elastyczność kodu.

Wyobraź sobie, że chcesz zrobić sto identycznych rzeźb z gliny. Masz dwa sposoby:
1. *Tradycyjny sposób* - formujesz każdą rzeźbę od postaw, co zajmuje dużo czasu i wysiłku.
2. *Lepszy sposób* - tworzysz jedną rzeźbę-matkę i używasz jej do formowania kolejnych, kopiując jej kształt.

Wzorzec Prototype działa dokładnie w ten sam sposób: zamiast tworzyć nowe obiekty od zera, tworzymy ich kopie (klony), co jest znacznie szybsze i bardziej wydajne.

---
Wzorzec Prototype jest użyteczny, gdy:
- Tworzysz nowy obiekt, który jest kosztowny (np. wymaga wielu obliczeń).
- Chcesz uniknąć skomplikowanej hierarchii klas z wieloma konstruktorami.
- Potrzebujesz dynamicznie konfigurowalnych obiektów.
- Używasz obiektów o dużej liczbie atrybutów i nie chcesz ich wszystkich ustawiać ręcznie.

**Implementacja wzorca Prototyp w Javie**

```
Najprostsza wersja wzorca wymaga interfejsu, który zapewnia metodę `clone()`:

public interface Prototype extends Cloneable {
	Prototype clone();
}

class Shape implements Prototype {
	... pola i metody ...

	@Override
	public Prototype clone() {
		return new Shape(this.color); // Tworzymy nowy obiek na pdst. istniejącego
	}

}
```

**Głębokie vs. Płytkie kopiowanie**
*Problem*: Jeśli nasza klasa ma obiekty zagnieżdżone (np. listy, tablice, inne obiekty), to domyślne klonowanie `super.clone()` kopiuje tylko **referencje**, a nie całe obiekty. Wtedy obie kopie wskazują na ten sam obiekt w pamięci.
*Rozwiązanie:* **Głębokie kopiowanie (ang. deep copy)**, w którym kopiujemy również wszystkie zagnieżdżone obiekty.

```
class PersonDeepCopy implements Cloneable {
	... pola i metody ...

	@Override
	protected Object clone() {
		return new PersonDeepCopy(this.name, new Address(this.address.street))
	}
}
```

1. Wzorzec Prototype pozwala na szybkie tworzenie kopii obiektów.
2. Możemy go zaimplementować za pomocą `Cloneable` i metody `clone()`.
3. Należy uważać na płytkie kopiowanie, gdy obiekt zawiera zagnieżdżone obiekty.
4. Głębokie kopiowanie wymaga ręcznego klonowania wszystkich składowych obiektów.

---
