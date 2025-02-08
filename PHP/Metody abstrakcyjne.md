Jeśli klasa posiada choćby jedną metodę abstrakcyjną, nazywana jest **klasą abstrakcyjną**.
Nie można utworzyć obiektu klasy abstrakcyjnej.
Jedynie, co możesz z nią zrobić to zdefiniować klasę, która będzie dziedziczyć po klasie abstrakcyjnej. Taka klasa musi posiadać własną implementację każdej metody abstrakcyjnej, która znajdowała się w klasie bazowej.

```
<?php

abstract class Pojazd {
	private $właściciel;

	public function setWłaściciel($właściciel) {
		$this->właściciel = $właściciel;
	}

	getWłaściciel(...) { ... }

	abstract public function jedz();
}

class Samochod extends Pojazd {

	public function __construct($właściciel) { $this->setWłaściciel($właściciel)};

	// Implementacja metody abstrakcyjnej rodzica
	public function jedz() {
		echo "Jedzie samochód.";
	}
}
```