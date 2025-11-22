To Unicode + jego kodowania (UTF-8, UTF-16, UTF-32) są odpowiedzialne za to, że komputery potrafią "czytać i pisać" niemal każdy język świata.

### Unicode

Unicode to uniwersalny standard mapowania znaków na liczby (kod punktowy).
Każdy znak = unikalna liczba (kod punktowy), np.
- `A -> U+0041`
- `ź -> U+017C` 
- `你 → U+4F60` 
- `😀 → U+1F600`

Unicode nie mówi, jak przechowywać znaki - tylko co one znaczą.
To jak słownik symboli. Ale żeby zapisać go w pamięci lub pliku, musimy wybrać kodowanie.

#### UTF = Unicode Transformation Format

Kodowanie = sposób zapisania liczby Unicode (U+xxxx) jako bajty.