Najprostsza funkcja
```
function przywitaj($name) {
	echo "Cześć, " . $name . "!";
}

przywitaj('Jan'); // Cześć, Jan!
```

**Domyślne wartości parametrów**
```
function przywitaj($name = "bezimienny") {
	echo "Cześć, $name!";
}

przywitaj(); // Cześć, bezimienny!
przywitaj("Anna"); // Cześć, Anna!;
```

**Argumenty nazwane (Named arguments) PHP 8**
PHP 8 pozwala przekazywać argumenty po nazwie, a nie tylko według kolejności.
```
function zamowienieKawy($ilosc, $typ, $rozmiar) {
	echo "Zamówiono $ilość kaw typu $typ w rozmiarze $rozmiar.";
}

zamowienieKawy(2, 'latte', 'big');

Wersja PHP 8
zamowienieKawy(typ: "expresso", rozmiar: "medium", ilosc: 1);
```

**Funkcje z określonymi typami danych**
Od PHP 7 można określić, jakiego typu mają być argumenty i co funkcja ma zwrócić.
```
function add(int $x, int $y): int {
	retunr $x + $y;
}

echo add(5, 10); // 15
```


**Funkcje z `mixed` PHP 8**
PHP 8 wprowadza nowy typ `mixed`, który oznacza, że funkcja może zwracać różne typy danych.
```
function test(): mixed {
	return rand(0, 1) ? "napis" : 123;
}

echo test(); // Może zwrócić napis lub liczbę
```


**Operator Null safe `?->`**
Jeśli funkcja może zwrócić `null`, w PHP 7 trzeba było to obsłużyć ręcznie.
`$user = null;`
`$addres = $user->getAddres(); // FATAL ERROR`

W PHP 8 `?->` chroni przed błędami
`$user = null`
`$addres = $user->getAddres(); // Zwraca null, ale nie ma błędu!`

---
**Funkcje strzałkowe `fn()`
```
function square($i) {
	return $i * 2;
}

echo square(5); // 10


Wersja skrócona fn()

$square = fn($i) => $i * 2;
echo square(5); // 10
```

**Funkcje z nieskończoną liczbą argumentów `...$args`**

