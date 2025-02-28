Ciasteczka do niewielki fragment informacji, który aplikacja internetowa może zapisać na komputerze użytkownika. Gdy przeglądarka łączy się ze stroną, w pierwszej kolejności szuka lokalnych cookies, odpowiednich dla danej witryny. Jeśli znajdzie - zostaną one przekazane serwerowi.

*Utworzenie ciasteczka (cookies)*
`setcookie($nazwa, $wartość, $koniec, $ścieżka, $domena, $bezpieczne)`
`setcookie` może przyjąć 6 argumentów, ale wymagane jest podanie tylko pierwszego.
- `$wartość` to wartość przypisana do ciasteczka
- `$koniec` oznacza datę wygaśnięcia ciasteczka
- `$scieżka` i `$domena` mogą być stosowane do określenia adresów, dla których cookie jest ważne.
- `$bezpieczne` oznacza że cookie nie będzie wysyłane przez zwykłe połączenie HTTP.

***Zastosowanie cookies***
```
// zapisanie oddania głosu jednorazowego
setcookie("oddano_glos", "1");

// w przypadku gdy głosować można raz dziennie
setcookie("oddano_glos", "1", time()+3600*24);

setcookie("username", "John", time() + 3600);
echo "Witaj, " . $_COOKIE['username']; // Witaj, John
```
