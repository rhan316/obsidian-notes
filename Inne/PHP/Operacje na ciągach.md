***Liczby losowe***
```
$i = mt_rand(1, 10);
echo "Wylosowana liczba z zakresu (1-10) to $i";
```
---
***Łączenie stringów***
```
$fruit = "apple";  
$demo = "Bardzo" . " lubię" . " placki " . $fruit;
```
Funkcja implode()
```
$dataA[0] = "18";  
$dataA[1] = "07";  
$dataA[2] = "1964";  
  
$allData = implode(" - ", $dataA); => 18 - 07 - 1964
```
---
***Szukanie podciągów***
Najczęściej stosowaną funkcją jest `strpos()`. Przyjmuje 2 argumenty. ciąg oraz ciąg szukany.
```
$wpisany_tekst = "Rozwijam swoją wiedzę w dziedzinie PHP.";

$czy = strpos($wpisany_tekst, "cholera");

if ($czy == FALSE) // nie znaleziono słowa cholera
   echo "Można wyświetlić: $wpisany_tekst.";
else // znaleziono szukany wyraz
   echo "Tekst zawiera wulgarne słownictwo.";
```
---
***Podział łańcucha znaków (String) na tablicę(array)***
Funkcja `explode()` w PHP służy do podziału łańcucha znaków na tablicę na podstawie określonego separatora.
`explode(string $separator, string $string, int $limit = PHP_INT_MAX): array`
- separator = znak lub ciąg znaków, który określa miejsce podziału.
- string = ciąg znaków do podziału.
- limit = (opcjonalny) określa maksymalną liczbę elementów w zwróconej tablicy.
```
$text = "jabłko,banan,gruszka";
$owoce = explode(",", $text);

print_r($owoce);

Wynik:
Array ( [0] => jabłko [1] => banan [2] => gruszka )
```
---
***Małe, duże litery, i inne***

*Zamiana na wielkie litery*
`strtoupper($value)` 

*Zamiana na małe litery*
`strtolower($value)`

*Zamiana pierwszych liter wyrazów na wielkie*
`ucwords($value)`

*Sprawdzanie liczby znaków w ciągu*
`strlen($value)`

*Usuwanie białych znaków z początku i końca ciągu*
`trim($value)`

---
