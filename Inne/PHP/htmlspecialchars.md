*Zasada ograniczonego zaufania*
Powinna nam ona przyświecać podczas konstruowania każdego serwisu internetowego.
Polega ona na tym, że użytkownikowi nie można ufać (czy. "ma złe intencje"). Przejawia się ona np. tym, że liczba pól formularza powinna być ograniczona do minimum, by zmniejszyć liczbę potencjalnych luk w bezpieczeństwie.

**Filtrowanie niebezpiecznych znaków**
Język PHP posiada wbudowane funkcje, mogące odfiltrować potencjalne niebezpieczeństwo. Jedną z nich, bardzo często przeze mnie stosowaną jest *htmlspecialchars($string)*.
```
$string = '<a href="adres">Niebezpieczny link</a> do <b>strony konkurencji</b>';
$string_h = htmlspecialchars($string);
$string_t = strip_tags($string);
echo $string_h . '<br>' . $string_t;
```