==Flex = układ w JEDNEJ osi.==
Poziomo lub pionowo.
Nigdy oba na raz.

Używamy, gdy:
- chcemy ułożyć rzeczy w linię
- wyrównać coś pionowo/poziomo
- zrobić kolumnę lub rząd
- zachować responsywność
```css
.container { display: flex; }
Boom! Kontener staje sie flexowym potworem.

flex-direction: row; /* poziomo (domyślnie) */
flex-direction: column; /* pionowo */
```
Zapamiętaj:
*row = lewo-prawo*
*column = góra-dół*

Jak to ogarniesz, masz 50% flexa w kieszeni.

### Centrowanie (magiczny duet)

W poziomie `justify-content: center;`
W pionie: `align-items: center;`
W obu:
```css
display: flex;
justify-content: center;
align-items: center;
```
To jest złoty graal.
Centruje wszystko. Zawsze jak czary.

### Rozkład przestrzeni
```json
justify-content: space-between; /pierwszy i ostatni do krawędzi
justify-content: space-around; /trochę miejsca po bokach
justify-conent: space-evenly; /równe przerwy
```
Użyjesz częściej niż myślisz.

### Rozciąganie elementów
```json
align-items: stretch;
```
Domyślnie - elementy dopasowują wysokość.

### Rozpierdolenie (czyli flex-grow/shrink/basis)
Flex potrafi MAGIĘ.

`flex-grow` - rośnij
```css
.item { flex-grow: 1; }
element rosnie, zeby wypelnic przestrzen
```

`flex-shrink` - zmniejszaj
```css
.item { flex-shrink: 1; }
```

`flex-basis` - bazowy rozmiar
```css
.item { flex-basis: 200px; }
```

Najczęściej używamy skrótu:
```css
.item { flex: 1; } /* grow = 1, shrink = 1, basis = 0 */
```

