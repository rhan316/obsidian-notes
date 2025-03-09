**Bcrypt** to funkcja haszująca używana do bezpiecznego przechowywania haseł. Jest szczególnie popularna w aplikacjach webowych, ponieważ została zaprojektowana z myślą o bezpieczeństwie i wydajności. *Bcrypt* jest odporny na ataki brute-force oraz ataki z użyciem tablic rainbow, ponieważ wykorzystuje sól (salt) raz jest powolny w obliczeniach, co utrudnia ataki.

### Jak działa Bcrypt?
1. **Sól (salt)**: Bcrypt automatycznie generuje sól, która jest losowym ciągiem znaków dodawanym do hasła przed haszowaniem. Sól jest przechowywana razem z hasłem, co sprawia, że nawet jeśli dwóch użytkowników ma to samo hasło, ich hashe będą rózne.
2. **Iteracje**: Bcrypt pozwala na określenie liczby iteracji (kosztu), co wpływa na czas potrzebny do wygenerowania hasła. Większa liczba iteracji oznacza większe bezpieczeństwo, ale również większe obciążenie procesora.
3. **Hash**: Wynikiem działania Bcrypt jest hash, który zawiera sól, liczbę iteracji oraz sam hash hasła. Dzięki temu można łatwo zweryfikować hasło, nie przechowując go w postaci jawnej.

### Jak działa Bcrypt pod maską?

**Generowanie soli**
Bcrypt automatycznie generuje sól (losowy ciąg znaków), która jest dodawana do hasła przed haszowaniem. Sól jest przechowywana razem z hashem, aby umożliwić weryfikację hasła bez konieczności przechowywania go w postaci jawnej.

**Haszowanie z użyciem funkcji Blowfish**
Bcrypt wykorzystuje zmodyfikowaną wersję algorytmu szyfrującego Blowfish do haszowania. Algorytm wykonuje wiele iteracji (zależnych od koszttu), aby spowolnic proces haszowania, co utrudnia ataki brute-force.

**Format wyniku**
Wynik haszowania Bcrypt składa się z:
- Algorytmu (np. `$2a$, $2b$, $2y$).
- Kosztu (liczba iteracji, np. `10`).
- Soli (22 znaki zakodowane w Base64). `$N9qo8uLOickgx2ZMRZoMye`
- Haszu (31 znaków zakodowanych w Base64). `IjZAgcfl7p92ldGxad68LJZdL17lhWy`
```hash
$2a$ 10 $N9qo8uLOickgx2ZMRZoMye IjZAgcfl7p92ldGxad68LJZdL17lhWy

$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
```
