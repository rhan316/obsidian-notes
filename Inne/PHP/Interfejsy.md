Interfejs to zestaw pól i metod, które klasa musi zaimplementować na własny sposób.

```
<?php

	interface Veichel {
		function run();
		function powerUp($fuel, $amount);
	}

class Maluch implements Veichel {
	private $fuel;
	private $amount;

	public function run() {
		echo "Maluch is running!";
	}

	public function powerUp($fuel, $amount) {
		if ($this->fuel === $fuel) {
			$this->amount += $amount;
		}
	}
}
```