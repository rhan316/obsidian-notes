Tworzymy nowe pliki dzięki `fopen()`.
Pierwszy argument to nazwa pliku, drugi to tryb otwarcia.
`$file = fopen("style.css", "w");`

**Zestawienie trybów otwarcia**

| Wartość | Opis                                                                                                                                                                                                                                                                                                                                                  |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `r`     | Otwiera tylko do odczytu; umieszcza wskaźnik pliku na jego początku                                                                                                                                                                                                                                                                                   |
| `r+`    | Otwiera do odczytu i zapisu; umieszcza wskaźnik pliku na jego początku                                                                                                                                                                                                                                                                                |
| `w`     | Otwiera tylko do zapisu; umieszcza wskaźnik pliku na jego początku i obcina plik do zerowej długości. Jeśli plik nie istnieje to próbuje go utworzyć.                                                                                                                                                                                                 |
| `w+`    | Otwiera do odczytu i zapisu. Reszta jak `w`                                                                                                                                                                                                                                                                                                           |
| `a`     | Otwiera tylko do zapisu; umieszcza wskaźnik pliku na jego końcu. Jeśli plik nie istnieje to próbuje go otworzyć.                                                                                                                                                                                                                                      |
| `a+`    | Otwiera do odczytu i zapisu. Tak samo jak w `a`                                                                                                                                                                                                                                                                                                       |
| `x`     | Tworzy i otwiera plik tylko do zapisu; umieszcza wskaźnik pliku na jego początku. Jeśli plik już istniej, wywołanie fopen() nie powiedzie się, zwróci FALSE i wygeneruje błąd na poziomie E_WARINING. Jeśli plik nie istnieje, spróbuje go utworzyć. To jest równoważne z określeniem flag O_EXCL\|O_CREAT stosowanym w wywołaniu systemowym open(2). |
| `x+`    | Tworzy i otwiera plik odczytu i zapisu. Reszta jak w `x`                                                                                                                                                                                                                                                                                              |

***Czytanie zawartości pliku***

`Fread`
Funkcja `Fread($uchwyt, $długość)` czyta z pliku określoną długość znaków. Czytanie kończy się, jeżeli osiągnięta zostanie $długość znaków, koniec pliku lub odczytanych zostanie $długość bajtów.

`Fgets`
Funkcja `Fgets($uchwyt)`. Czyta jedną linię pliku, dopóki nie napotka znacznika przejścia kolejnej linii. Żeby odczytać cały plik, wystarczy użyć pętli.
```
$file = fopen("values.txt", "r");

$data = "";

while(!feof($file)) {
	$line = fgets($file);
	$data .= $line;
}
```

`Fgetc` jest bardzo podobna w użyciu do fgets, z tą różnicą, że czytamy po jednym znaku.


| Właściwość            | `file_get_contents()`                             | `fgets()`                                   |
| --------------------- | ------------------------------------------------- | ------------------------------------------- |
| Zwracana wartość      | Cały plik jako jeden ciąg znaków                  | Pojedyncza linia po linii z pliku           |
| Wymaga otwarcia pliku | Nie, plik jest otwierany i zamykany automatycznie | Tak, wymaga użycia `fopen()` i `fclose()`   |
| Zastosowanie          | Małe/średnie pliki                                | Duże pliki                                  |
| Wydajność             | Szybkie dla małych plików, ale zużywa pamięć      | Bardziej wydajne dla dużych plików          |
| Elastyczność          | Mniejsza (czyta cały plik naraz)                  | Większa (możliwość czytania linia po linii) |

---
***Zapisywanie zawartości***
Aby zapisać dane do pliku używamy funkcji `fwrite()`. Jest ona równoważna z instrukcją fputs().

`fwrite($uchwyt, $treść)`
Funkcja zapisuje do pliku tekst zapisany w zmiennej $treść. Podczas wywoływania można dodać trzeci, opcjonalny argument - $długość. Jeśli go zamieścimy, do pliku zostanie zapisanych maksymalnie $długość znaków.
```
// tryb a umożliwia zapis na końcu pliku
$file = fopen("tekst.txt", "a");

$data = "Przykładowa treść, którą umieścimy w pliku.";

fwrite($file, $data);

```