***ZMIENNE***

~={8}const NR_TEL = "151351"=~ Stała, niemutowalna. Globalne na cały skrypt. Definicja w funkcji dzięki - define()
~={12}$nr_tel = "4634626"=~ Zmienna, mutowalna. Zakres lokalny i globalny.
~={red}$_POST, $_GET =~ Superglobalne zmienne. Przechowują dane przesyłane przez formularze i adresy URL
! Dane z `$_POST` i `$_GET` mogą być manipulowane przez użytkownika, więc zawsze trzeba je filtrować i walidować.

----
***Operatory inkrementacji i dekrementacji***

```
$i++ postinkrementacja, zwiększa wartość zmiennej o 1
++$i preinkrementacja, zwiększa wartość zmiennej o 1
```
Różnica między pre- i post- inkrementacją leży w momencie zwiększenia wartości. Pre inkrementacja zwiększa wartość przed wykonaniem polecenia, natomiast post inkrementacja zwiększa wartość po wykonaniu polecenia.

---
***var_dump(value)***

Zrzuca zmienną, tablicę lub obiekt na ekran wraz ze wszystkim jej parametrami (typ, długość itp.).
`$nr_tel = "3521515"; var_dump($nr_tel); ===> string(7) "3521515"`

---
***Tablice asocjacyjne w PHP***
Jest to tworzenie własnych indeksów dla tablicy zamiast `[0], [1] itd `. Poprawia to czytelność tablicy.
```
$user['name'] = "Jan";
$user['email'] = "jan124@example.com";
$user['city'] = "London";
```

**Zagnieżdżone tablice asocjacyjne**
```
$users = array();  
  
$user['name'] = "Jan";  
$user['age'] = 18;  
$user['email'] = "jan123@example.com";  
  
$users['Jan'] = $user;  
  
$anotherUser['name'] = "Ann";  
$anotherUser['age'] = 25;  
$anotherUser['email'] = "user444@gmail.com";  
  
$users['Ann'] = $anotherUser;


echo $users['Jan']['age'] . "<br>";  ==> 17
echo $users['Ann']['email'] . "<br>"; ==> user444@gmail.com
```

---
***Pętla foreach***

Pętla for-each służy do iterowania po tablicach i obiektach implementujących interfejs `Traversable`.

```
foreach ($array as $value) {
	instrukcje
}

W PHP możemy również pobierać klucze (indeksy w tablicy asocjacyjnej)

foreach($array as $key => $value) {
	instrukcje
}

$person = [
	"name" => "Jan",
	"age" => 30,
	"city" => "Warszawa"
];

foreach($person as $key => $value) {
	echo "$key: $value"
}

name: Jan
age: 30
city: Warszawa
```

*PHP iteruje po kopiach wartości (chyba że użyjesz `&`)*

```
$numbers = [1, 2, 3];

foreach($numbers as $num) {
	$num *= 2; // Modyfikujemy num, ale nie zmienia to tablicy
}

Jeśli chcesz zmieniać orginalne wartości, musisz użyć referencji `&`

$numbers = [1, 2, 3];

foreach($numbers as &$num) {
	$num *= 2 // Teraz zmiana wpłynie na orginalną tablicę
}

!!! UWAGA Jeśli po foreach będziesz jeszcze korzystać z tej zmiennej, może ona nadal wskazywać na referencję ostatniego elementu. Dlatego lepiej zawsze użyć unset($num) po pętli.
```

---
