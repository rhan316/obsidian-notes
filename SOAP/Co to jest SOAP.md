SOAP (Simple Object Access Protocol) to protokół komunikacyjny oparty na XML, wykorzystywany do przesyłania wiadomości między różnymi aplikacjami, niezależnie od używanego języka programowania czy platformy. 

SOAP to protokół sieciowy, który umożliwia wymianę danych między aplikacjami za pomocą komunikatów XML. Jest często wykorzystywany w tworzeniu usług sieciowych (Web Services) i jest popularny w środowiskach, gdzie wymagana jest wysoka niezawodność i bezpieczeństwo. SOAP działa niezależnie od transportu - najczęściej używany jest z HTTP, może może również działać na innych protokołach, jak SMTP.

SOAP jest bardziej złożony i cięższy w porównaniu do REST, ponieważ opiera się na ustrukturyzowanym XML i ma specyfikacje wspierające takie funkcje, jak:
1. Bezpieczeństwo (WS-Security)
2. Transakcje (WS-Atomic Transaction)
3.  Routing i adresowanie (WS-Addressing)

Kluczowe elementy SOAP:
1. **SOAP Envelope:** Zawiera strukturę wiadomości, określa, co jest w wiadomości, jak powinna być przetwarzana oraz jakie są jej elementy
2. **SOAP Header**: Nagłówek może zawierać dodatkowe informacje, takie jak dane uwierzytelniające.
3. **SOAP Body**: Właściwa treść wiadomości (dane, które chcemy przekazać).
4. **SOAP Fault**: Służy do raportowania błędów w komunikacji