W PHP możemy dołączać inne pliki do kodu głównego, co pomaga w organizacji kodu i ponownym używaniu funkcji, nagłówków, stylów itd.

`include 'header.php';` => wstawia zawartość pliku header.php do kodu.
`require 'config.php';` => robi to samo, ale z wymaganiem, że plik musi istnieć.

`include` dołącza plik, ale nie zatrzymuje działania programu przy błędzie. PHP rzuci ostrzerzenie `Warning`, ale skrypt będzie działać dalej.

`require` dołącza plik i zatrzymuje program przy błędzie. Rzuci fatalny błąd `Fatal error`.

---
`include_once` => Dołącza plik tylko raz (zapobiega duplikacji kodu).
`require_once` => To samo co `require`, ale tylko raz.
