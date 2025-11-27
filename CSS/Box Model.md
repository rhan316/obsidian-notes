Jeśli nie ogarniesz Box Modelu - wszystko dalej będzie wyglądało jak sraczka.

### Każdy element to pudełko, które ma 4 warstwy:
```css
┌───────────────────────────────┐
│           margin              │
│  ┌──────────────────────────┐ │
│  │        border            │ │
│  │  ┌────────────────────┐  │ │
│  │  │      padding       │  │ │
│  │  │  ┌──────────────┐  │  │ │
│  │  │  │   content    │  │  │ │
│  │  │  └──────────────┘  │  │ │
│  │  └────────────────────┘  │ │
│  └──────────────────────────┘ │
└───────────────────────────────┘
```

`content` - tekst, obraz, cokolwiek
`padding` - odstęp wewnątrz
`border` - ramka
`margin` - odstęp na zewnątrz

### Święta reguła:

***Szerokość elementu = content + padding + border***
I dlatego wszystko ci się rozjeżdża.
Ale jest magiczna rzecz:
```css
box-sizing: border-box;
```
To sprawia, że:
***width = content + padding + border = STAŁE***
nic ci nie puchnie.
UŻYWAJ TEGO ZAWSZE!

```json
.box {
	width: 200px; / tylko content
	padding: 20px; / doda się do szerokości
	border: 5px solid black; / to też się doda
}
```
REALNA szerokość = 200px (content) + 40px (padding) + 10px (border) ==> 250px
Czyli 200px to ściema.
Tak naprawdę element jest WIĘKSZY.

#### A teraz z border-box:
```json
.box {
	width: 200px;
	padding: 20px;
	border: 5px solid black;
	box-sizing: border-box;
}
```
REALNA szerokość = 200px. koniec.
Bo padding i border mieszczą się wewnątrz tej wartości.

