**SHA (Secure Hash Algorithm)** to rodzina funkcji kryptograficznych używanych do generowania bezpiecznych skrótów danych. W aplikacjach webowych, np. Spring Boot, SHA jest wykorzystywane do:
- Przechowywania haseł.
- Sprawdzania integralności plików.
- Generowanie podpisów cyfrowych.

### Jak działa SHA?
SHA działa podobnie do MD5, ale jest bezpieczniejszy. Wejściowe dane są przekształcane w ciąg znaków o stałej długości (np. 256 bitów dla SHA-256).

**Algorytm SHA składa się z kilku kroków**

**Padding (uzupełnianie danych)**
- dane są uzupełniane do wielokrotności 512 lub 1024 bitów (w zależności od wersji SHA).
- do końca dodawana jest jedynka `1` , a potem zera `0`.
- ostatnie 64 bity zawierają długość oryginalnej wiadomości.

**Podział na bloki**
Wejście jest dzielone na bloki (512 bitowe dla SHA-256).

**Inicjalizacja rejestrów**
SHA używa kilku 32- lub 64- bitowych rejestrów, które są inicjalizowane stałymi wartościami.

**Mieszanie danych (round functions)**
Każdy blok przechodzi przez N rund przekształceń, używając operacji takich jak:
- Funkcje logiczne `AND, OR, XOR, NOT`
- Przesunięcia bitowe
- Dodawanie modułowe

**Generowanie hasha**
Po przejściu przez wszystkie bloki wynik jest konwertowany na ciąg heksadecymalny.

