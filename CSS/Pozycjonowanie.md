Domyślnie elementy w CSS układają się:
- *od góry do dołu* (block: `div, p, h1` itd.)
- *od lewej do prawej* (inline: `span, a` itd.)
To jest tzw. ***Normal Flow***
Dopóki nie ruszysz `position`, przeglądarka sam decyduje gdzie co stoi.

### `position`
Masz 5 podstawowych wartości:
- `static` -> domyślnie, "nic nie kombinuję"
- `relative` -> przesuwam się trochę względem swojego miejsca
- `absolute` -> wyrywam się z normalnego układu i przyklejam gdzieś
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
	position: relative;
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