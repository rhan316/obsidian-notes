Domyślnie elementy w CSS układają się:
- *od góry do dołu* (block: `div, p, h1` itd.)
- *od lewej do prawej* (inline: `span, a` itd.)
To jest tzw. ***Normal Flow***
Dopóki nie ruszysz `position`, przeglądarka sama decyduje gdzie co stoi.

### `position`
Masz 5 podstawowych wartości:
- `static` -> domyślnie, "nic nie kombinuję"
- `relative` -> przesuwam się trochę względem swojego miejsca
- `absolute` -> wyrywam się z normalnego układu i przyklejam się gdzieś
- `fixed` -> przyklejony do końca przeglądarki
- `sticky` -> hybryda: trochę normalny, trochę przyklejony podczas scrolla

#### `position: static` (czyli default)
Jeśli nic nie ustawisz, jest `static`
```css
.box {
	position: static; // domyslnie, nawet jak tego nie napiszesz
}
```

#### `position: relative` - stoję tu, ale przesuwam się trochę
Element zostaje w normalnym przepływie, ale możesz go przesunąć:
```css
.box {
	position: relative;
	top: 10px; // przesuniety w dol o 10px
	left: 20px; // przesuniety w prawo o 20px (bo left dodatni = w prawo)
}
```
Klucz:
- zajmuje dalej swoje miejsce jak wcześniej
- tylko wizualnie się przesuwa
Często używane jako "kotwica" dla `absolute`.

### `position: absolute` - mam wyjebane na normalny układ
Element:
- wypada z normalnego przepływu (inne elementy udają, że go nie ma)
- jest ustawiany względem ***najbliższego przodka***, który ma `position != static` czyli `relative, absolute, fixed, sticky`
- jak nie znajdzie takiego, to leci względem `<body>` / okna dokumentu.
```html
<div class="parent">
	Parent
	<div class="child">Child</div>
</div>
```
```css
.parent {
	position: relative; // Kotwica
	width: 300px;
	height: 200px;
}

.child {
	position: absolute;
	top: 10px;
	right: 10px;
}
```
Tutaj `.child` jest w prawym górnym rogu wewnątrz `.parent`.
Gdyby `.parent` nie miał `position: relative`, dziecko ucieknie i ustawi się względem całej strony.

Typowe użycie:
- tooltipy
- badge "NEW" w rogu
- dropdowny

---
### `position: fixed` - przyklejam się do ekranu
Element:
- zawsze liczy pozycję względem okna przeglądarki
- nie rusza się przy scrollowaniu
```css
.navbar {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
}
```
Typowe:
- sticky nav
- floating button "back to top"
- chat bubbles w rogu
---
### `position: sticky` - dopóki nie przewiniesz
Hybryda:
- dopóki nie przewiniesz - zachowuje się jak `relative`
- kiedy dojedziesz do np. `top: 0` - przykleja się jak `fixed`
```css
.header {
	position: sticky;
	top: 0;
}
```
Działa wewnątrz kontenera, nie całej strony.
Fajna rzecz, jak chcesz, żeby np. nagłówek sekcji trzymał się góry podczas scrollowania danego kontenera.

### `top, right, bottom, left`

Działają tylko, gdy: `position != static`
Interpretacja:
- `top: 10px` -> przesuń w dół od góry o 10px
- `left: 10px` -> w prawo od lewej o 10px
- `right: 10px` -> w lewo od prawej o 10px
- `bottom: 10px` -> w górę od dołu o 10px
Tak, jest to upierdliwe, przyzwyczaisz się.

### `z-index` - kto jest na wierzchu

Im większy `z-index`, tym bardziej na froncie.
Działa tylko dla elementów, które mają `position` różne od `static`:
```css
.modal {
	position: fixed;
	z-index: 9999;
}
```
Masz dwa elementy, jeden zachodzi na drugi?
Większy `z-index` wygrywa.

### Typowe pułapki (czyli gdzie ludzie krzyczą "czemu to nie działa?!")

1. `position: absolute` i brak `position` na rodzicu -> element odjeżdża względem całej strony.
2. `z-index` nie działa -> bo element ma `position: static`
3. za dużo `absolute` wszędzie -> layout zaczyna się sypać na różnych rozdzielczościach

Dlatego dziś częściej robi się layouty na: `flexbox i grid`
A `position` używa się do detali, nakładek, tooltipów, overlayów.

