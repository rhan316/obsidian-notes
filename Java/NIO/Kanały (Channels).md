Kanał to interfejs do odczytu i zapisu danych, który działa na niższym poziomie niż klasyczne strumienie. Jest to jednostka reprezentująca połączenie między źródłem a celem danych (np. plikiem, socketem, pamięcią, itp.).

Główne cechy kanałów:
- **Dwukierunkowość** - Kanały mogą obsługiwać zarówno odczyt, jak i zapis (w przeciwieństwie do wielu strumieni, które są albo do odczytu, albo do zapisu).
- **Bufory** - Wszystkie operacje odbywają się na połączeniu między buforami. Bufor (ang. buffer) to miejsce w pamięci, gdzie przechowywane są dane podczas ich przetwarzania.
- **Nieblokujące operacje** - Kanały mogą działać w trybie nieblokującym, co oznacza, że wątek nie musi czekać, aż operacja się zakończy.


| Nazwa                          | Opis                                                                                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ~={yellow}FileChannel=~        | Służy do odczytu, zapisu modyfikacji plików. Działa na poziomie plików, umożliwiając losowy dostęp (np. możesz przeskoczyć do dowolnego miejsca w pliku). |
| ~={magenta}SocketChannel=~     | Obsługuje połączenia sieciowe TCP. Możesz nawiązać połączenie z serwerem lub obsługiwać połączenia klienta.                                               |
| ~={green}ServerSocketChannel=~ | Działa jak serwer nasłuchujący na połączenia od klientów. Umożliwia tworzenie wielowątkowych aplikacji serwerowych.                                       |
| ~={red}DatagramChannel=~       | Obsługuje komunikację sieciową w protokole UDP.                                                                                                           |
| ~={8}Pipe=~                    | Specjalny kanał do komunikacji między dwoma wątkami w tej samej aplikacji (jednokierunkowa rura danych).                                                  |
