Grid = układ w DWÓCH osiach naraz.
To layout-level boss.

### Aktywacja grida
```css
.container { display: grid; }
```

### Definicja kolumn i wierszy

*Kolumny:*
```json
grid-template-columns: 1fr 1fr 1fr; / 3 kolumny, równe
```

*Wiersze:*
```json
grid-template-rows: auto auto
```
`fr` = część dostępnego miejsca -> najważniejsza jednostka w Gridzie.

### Automatyczne kolumny - responsywność pro level
```json
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```
To sprawia, że elementy układają się jak w nowoczesnej stronie...
bez flexowych triksów.

### Gaps (przerwy, nie marginesy)
```json
gap: 20px;
```
Flex tego nie miał przez lata. Grid to ocalił.

### Pozycjonowanie w Gridzie (level boss)
```json
.item {
	grid-column: 1 / 3; / zajmij 2 kolumny
	grid-row: 1 / 2; / zajmij 1 wiersz
}
```
Możesz przeciąć layout jak chcesz.
