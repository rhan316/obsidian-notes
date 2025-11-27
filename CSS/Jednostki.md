
### Jednostki absolutne (sztywne, jak regulamin w banku)

To te, które NIE zależą od ekranu ani użytkownika.

##### `px` - piksele. 
Najczęściej używane. Punkt odniesienia dla wszystiego.

##### `cm, mm, in` - centymetry, milimetry, cale. 
Brzmi fajnie, w praktyce prawie nikt tego nie dotyka, bo ekrany mają różne DPI.

##### `pt, pc` Punkt typograficzny i pica. 
Jeszcze bardziej niszowe.

### Jednostki względne (mądrzejsze, bardziej elastyczne)

To jest to, czego frontenderzy naprawdę używają.

##### `em` - Odwołuje się do font-size rodzica
Czyli skaluje się wg kontekstu.
`1em` = rozmiar czcionki rodzica
`2em` = dwa razy tyle

##### `rem` Najlepsza jednostka w świecie ludzi normalnych.
Odwołuje się do font-size HTML (root).
Zawsze stabilna, przewidywalna.
`1rem` = font-size na `<html>`
`2rem` = dwa razy tyle
*Nie dziedziczy jak `em`, więc nie robi bałaganu*

##### `%` Procent rodzica - często używane w width/height.

### Jednostki viewportu (czyli zależne od okna przeglądarki)

To te, które robią responsywność bez płaczu.

`vw` => viewport width
`1vw` = 1% szerokości okna

`vh` => viewport height
`1vh` = 1% wysokości okna

`vmin / vmax`
`vmin` = mniejszy z wymiarów ekranu
`vmax` = większy
Użyteczne do centralizacji full-screen.

### Jednostki frakcyjne (w CSS Grid)

`fr` Najbardziej zajebista jednostka w Gridzie.
Np.
```css
grid-template-columns: 1fr 2fr;

Czyli:
- pierwsza kolumna: 1 czesc
- druga kolumna: 2 czesci
  => razem 3 czesci ==> 33% + 66%
```
Flex tego nie ma. Grid ma.

### Nietypowe, ale potężne (CSS Level 4)

`ch`
Szerokość jednego znaku "0" w fontcie.
Mega dobre dla pól tekstowych.

`ex`
Wysokość litery "x".
Rzadziej potrzebne.