Reprezentuje ścieżkę do pliku lub katalogu w systemie plików. Jest to nowoczesna i bardziej elastyczna alternatywa dla klasy `File java.io`. wprowadzona w Javie 7 jako część NIO.


| Cecha                        | Opis                                                                                                                                                      |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Abstrakcja ścieżki           | `Path` może reprezentować zarówno *ścieżkę absolutną*, jak i *ścieżkę względną* Jest bardziej precyzyjny niż `File`, obsługując np. różne systemy plików. |
| Łączenie z systemem plików   | Obiekt `Path` jest tworzony przez system plików za pośrednictwem klasy `FileSystems`.                                                                     |
| Łatwe operacje na plikach    | `Path` pozwala na manipulacje segmentami ścieżki, np. pobieranie katalogu nadrzędnego, rozdzielenie elementów ścieżki czy tworzenie nowych ścieżek        |
| Obsługa symbolicznych linków | `Path` ma funkcję dedykowane do obsługi symbolicznych i twardych linków.                                                                                  |
