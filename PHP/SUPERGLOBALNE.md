Superglobalne zmienne to specjalne tablice w PHP, które zawierają informacje o żądaniach HTTP, sesjach, plikach cookie, środowisku serwera i innych danych. Są one dostępne **wszędzie** w skrypcie, niezależnie od tego, czy jesteś w funkcji, metodzie klasy czy poza nimi.

**Lista superglobalnych zmiennych w PHP**
Oto najważniejsze superglobalne zmienne:

`$_GET` - zawiera dane przesyłane w URL (metoda GET).
`$_POST` - zawiera dane przesłane w treści żądania (metoda POST).
`$_COOKIE` - zawiera dane z plików cookie.
`$_SESSION` - zawiera dane sesji.
`$_SERVER` - zawiera informacje o serwerze i żądaniu HTTP.
`$_FILES` - zawiera informacje o przesyłanych plikach.
`$_REQUEST` - zawiera dane z `$_GET`, `$_POST` i `$_COOKIE`.
`$_ENV` - zawiera zmienne środowiskowe.

**Dlaczego są globalne?**
Superglobalne zmienne są dostępne w każdym zakresie, ponieważ:
- Są automatycznie tworzone przez PHP.
- Zawierają kluczowe informacje o żądaniu HTTP, sesjach, plikach cookie itp.
- Ułatwiają dostęp do tych danych bez konieczności przekazywania ich jawnie między funkcjami lub klasami.

**Uwaga dotycząca bezpieczeństwa**
Superglobalne zmienne są często używane do przetwarzania danych od użytkownika, dlatego należy je **zawsze walidować i filtrować**, aby uniknąć ataków, takich jak SQL Injection czy XSS.