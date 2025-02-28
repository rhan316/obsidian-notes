**Podstawowe funkcje**

`date(format)` zwraca bieżąca datę i czas w określonym formacie.
`echo date("Y-m-d H:i:s");` // np. 2023-10-05 14:30:00

`time()` zwraca znacznik czasu (timestamp) jako liczbę sekund od 1 stycznia 1970 (Unix Epoch).
`echo time();` // np. 46262615151

`strtotime(time_string)` konwertuje tekstową reprezentację daty na znacznik czasu.
`echo strtotime("next Monday");` Np. 3525111666

Funkcja `strtotime()` analizuje tekstowy opis daty/czasu i próbuje go zinterpretować na podstawie względnych lub bezwzględnych wyrażeń.

`strtotime("+1 day")` - jutro
`strtotime("-2 weeks")` - 2 tygodnie temu
`strtotime("last Friday")` - ostatni piątek

`strtotime("2023-10-05")` - konkretna data
`strtotime("14:30:00")` - konkretna godzina

`strtotime("next monday +1 week")` - poniedziałek za 2 tygodnie
`strtotime("2023-10-05 +3 days")` - 3 dni po 5 października 2023

---
**Formatowanie daty i czasu**

`Y` -> rok (np. 2023)
`m` -> miesiąc (np. 01, 11)
`d` -> dzień(np. 03, 21)
`H` -> godzina (24-godzinny format, np. 00 do 23)
`i` -> minuty
`s` -> sekundy
`D` -> dzień tygodnia
`l` -> pełna nazwa tygodnia (np. Monday)

`echo date("l, d F Y H:i:s")` np. Thursday, 05 October 2023 14:30:00

---
**Klasa `DateTime`**

Tworzenie obiektu
`$date = new DateTime();` bieżąca data i czas
`$date = new DateTime("2023-10-05 14:30:00")` konkretna data

Formatowanie
`echo $date->format("Y-m-d H:i:s")` 2023-10-05 14:30:00

Modyfikacja
`$date->modify("+1 day")` dodaj 1 dzień
`echo $date->format("Y-m-d)`np. 203-10-06

---
**Różnice między datami**
```
Użycie DateTime::diff()

$date1 = new DateTime("2023-10-05");
$date2 = new DateTime("2023-10-10");
$interval = $date1->diff($date2);
echo $interval-days; Różnica w dniach (np. 5)
```
