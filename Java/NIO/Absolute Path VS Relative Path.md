W systemie plików mamy dwa sposoby określania ścieżek do plików i katalogów:
**Absolute Path (ścieżka absolutna)**
**Relative Path (ścieżka względna)**
Java NIO `java.nio.file` obsługuje oba te typy ścieżek za pomocą interfejsu `Path`.

*Absolute Path* to ścieżka do pliku lub katalogu, zaczynająca się od **root** systemu plików np. `C:\` `/` itp.
Przykłady ścieżek absolutnych
Windows:
`C:\Users\John\Documents\report.pdf`
`D:\Projects\Java\Main.java`

Linux/macOS:
`/home/john/documents/report.pdf`
`/usr/local/bin/script.sh`


*Relative Path* to ścieżka, która jest określana względem bieżącego katalogu (`current working directory`)
Przykłady ścieżek względnych:
`Documents/report.pdf`
`Projects/Java/Main.java`
`../config/settings.json`


Ścieżkę względną możemy przekonwertować na absolutną używając `toAbsolutePath()`
```
var relPath = Paths.get("Documents", "file.txt");
var absPath = relPath.toAbsolutePath();

Wynik:
C:\Users\John\Documents\file.txt
```


Możemy łączyć ścieżki względne z absolutnymi za pomocą `resolve()`
```
var basePath = Path.of()
```


| Cecha                         | Absolute Path                      | Relative Path                              |
| ----------------------------- | ---------------------------------- | ------------------------------------------ |
| Definicja                     | Pełna ścieżka do root              | Ścieżka względem bieżącego katalogu        |
| Np. Windows                   | `C:\Users\John\Documents\file.txt` | `Documents\file.txt`                       |
| Np. Linux                     | `/home/john/documents/file.txt`    | `documents/file.txt`                       |
| Zależność od lokalizacji?     | Nie                                | Tak                                        |
| Czy zawiera root? `C:\`       | Tak                                | Nie                                        |
| Jak uzyskać absolutną wersję? | (nie zmienia się)                  | `toAbsolutePath()` konwertuje na absolutną |
