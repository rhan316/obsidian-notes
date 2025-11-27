Jak nie ogarniasz selektorów -> frameworki cię zjedzą.

NAJWAŻNIEJSZE:
```java
"Element:"
div { }
p {}

"Klasa:"
.title { }

"ID:"
#header { }
```
Używaj rzadko. Nie zachowuje się grzecznie.

---
```java
"Selektor potomka (spacja):"
.menu .item { }
= .item wewnątrz .menu

"Selektor bezpośredniego dziecka >":
.menu > .item { }
= tylko pierwsza generacja

"Sąsiad +":
.box + .info { }
= .info tuż po .box

"Rodzeństwo ~":
.box ~ .info { }

"Pseudoklasy:"
button:hover { }
li:nth-child(3) { }
input:focus { }
```

### Specyficzność (czyli: kto wygrywa bitwę o styl)
To klucz. Jak tego nie znasz -> walniesz:
`!important` jak desperat. A tego NIE ROBIMY.

### Priorytet od najmocniejszego do najsłabszego:
1. `!important` -> broń masowej zagłady (nie używaj lub rzadko)
2. `style="..."` -> inline style
3. `#id`
4. `.class, :pseudo-class`
5. `element (tag)`
6. `* (globalny)`

Np.
```css
h1 { color: red; }
.title { color: blue; }
#header { color: green; }
```
Jeśli element wygląda tak:
```html
<h1 id="header" class="title">Text</h1>
Wygrywa zielony, bo ID > klasa > tag
```

```css
.nav .btn { color: red; } /* mocny */
.btn { color: blue; } /* słabszy
```
`.nav .btn` będzie zawsze wygrywać.

**Zapamiętaj raz na zawsze: Im bardziej szczegółowy selektor -> tym mocniejszy**
