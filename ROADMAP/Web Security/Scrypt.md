**Scrypt** to algorytm do bezpiecznego hashowania haseł zaprojektowany tak, aby był odporny na ataki słowne (brute-force) i ataki siłowe. W Spring Boot można używać do bezpiecznego przechowywania haseł użytkowników.

### Dlaczego potrzebujemy Scrypt?
Kiedy użytkownik loguje się do aplikacji, nie przechowujemy jego hasła w postaci jawnej (plain-text), ponieważ gdyby baza danych została skompromitowana, atakujący natychmiast uzyskałby dostęp do wszystkich kont.
*Złe rozwiązanie* - Trzymanie haseł w postaci jawnej.
*Dobre rozwiązanie* - Haszowanie i solenie haseł przed ich zapisaniem.

***Czym Scrypt różni się od innych algorytmów?***
Scrypt został zaprojektowany jako alternatywa dla `bcrypt i PBKDF2`, ale jest znacznie bardziej odporny na ataki sprzętowe (np. ataki na kartach graficznych - GPU). W odróżnieniu od bcrypta, *Scrypt* wymaga dużych zasobów pamięci RAM, co utrudnia ataki siłowe na dużą skalę.

| Algorytm                  | Odporność na ataki GPU? | Wykorzystywanie RAM | Szybkość                        |
| ------------------------- | ----------------------- | ------------------- | ------------------------------- |
| `MD5`, `SHA-1`, `SHA-256` | Łatwo złamać na GPU     | Brak                | Bardzo szybki                   |
| `PBKDF2`                  | Niska odporność         | Średnie             | Wolniejszy niż SHA              |
| `bcrypt`                  | Odporny na GPU          | Niski RAM           | Wolniejszy                      |
| `Scrypt`                  | Najlepsza odporność     | Wysokie             | Wolniejszy, ale bezpieczniejszy |
### Jak działa Scrypt?
Scrypt działa na kilku krokach:
1. **Solenie (salt)** -> do hasła dodawany jest losowy ciąg znaków, aby utrudnić ataki siłowe.
2. **Iteracyjne haszowanie** -> hasło jest przetwarzane przez algorytm wielokrotnie, zwiększając czas potrzebny do złamania.
3. **Pamięciowe obliczenia** -> algorytm wymaga dużej ilości RAM, co sprawia, że ataki na GPU są nieefektywne.
4. **Zwrócenie skrótu (hash)** -> wynikowy hash jest przechowywany w bazie danych zamiast hasła użytkownika.

