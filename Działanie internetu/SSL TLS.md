**SSL (Secure Sockets Layer) i TLS (Transport Layer Security)** to protokoły kryptograficzne, które zabezpieczają komunikację w internecie. Są jak stróże, którzy chronią przesyłane dane przed podsłuchiwaniem, manipulacją i fałszowaniem.

---
**Różnica między SSL a TLS**

*SSL* -> Starsza wersja protokołu. Pierwsza wersja (SSL 2.0) została wprowadzona w 1995 roku, ale jest już przestarzała i podatna na ataki. Ostatnia wersja to SSL 3.0, która została zastąpiona przez TLS.

*TLS* -> Nowsza i bardziej bezpieczna wersja. TLS wprowadza poprawki błędów SSL i dodaje nowe funkcje, takie jak silniejsze algorytmy szyfrowania. Aktualnie TLS 1.3 jest najnowszą wersją.

---
**Jak działa SSL/TLS - Wersja z analogią**

**Spotkanie  i wymiana kluczy (Handshake).**
	Wyobraź sobie, że Ty i ktoś inny chcecie się komunikować w tajemnicy. Zanim zaczniecie rozmowę, ustalacie wspólny szyfr (np. alfabet, w którym A to Z, B to Y itd.).
		W TLS na początku klient (np. przeglądarka) i serwer ustalają zasady szyfrowania (algorytmy i klucze). Robią to w taki sposób, że nikt podsłuchujący nie może poznać tych kluczy.

**Szyfrowanie symetryczne - Bezpieczne pisanie listów**
	Po ustaleniu wspólnych zasad, każda wiadomość jest zamykana w kopercie (szyfrowana). Klucz do jej otwarcia mają tylko dwie strony: nadawca i odbiorca.
		Szyfrowanie symetryczne jest szybkie i skuteczne - to jak używanie wspólnego sejfu z jednym kluczem.

**Autentyczność - Czy to na pewno on?**
	Serwer "podpisuje" swoje dane za pomocą certyfikatu SSL/TLS (jak pieczęć notarialna na dokumencie). Certyfikat jest wystawiany przez zaufaną instytucję (CA) abyś wiedział, że nie rozmawiasz z podszywającym się oszustem.

**Bezpieczna transmisja**
	Po  zakończeniu handshaku wszystkie dane są szyfrowane, więc nawet jeśli ktoś przechwyci wiadomość, zobaczy jedynie losowy ciąg znaków.

---
**Techniczne komponenty SSL/TLS**

| Nazwa                      | Opis                                                                                            | Algorytmy                                    |
| -------------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Szyfrowanie symetryczne    | Wykorzystuje ten sam klucz do szyfrowania i deszyfrowania.                                      | AES (Advanced Encryption Standard), ChaCha20 |
| Szyfrowanie asymetryczne   | Używa dwóch kluczy: publicznego (do szyfrowania) i prywatnego (do deszyfrowania)                | RSA, ECDSA                                   |
| Certyfikaty SSL/TLS        | Są to pliki cyfrowe potwierdzające tożsamość serwera                                            | Wystawiane przez urzędy certyfikacji         |
| Algorytmy skrótu (Hashing) | Używane do zapewnienia integralności danych (sprawdzanie, czy wiadomość nie zostaje zmienniona) | SHA-256, SH-3                                |
