
Tutaj nie porównujesz dwóch `stringów`.
Ty porównujesz:
- ciąg znaków znajdujący się w buforze wejściowym
- do liter w stałym napisie, np. `"true"`
I robisz to bez tworzenia żadnych obiektów String.
To jest mega szybka technika, stosowana w tokenizerach, lexerach i parserach - oszczędza pamięć i czas.

### Jak to działa krok po kroku?
```java
private boolean match(String w) {
	int len = w.length();
	if (index + len > length) return false;
	
	for (int i = 0; i < len; i++) 
		if (data.charAt(index + i) != w.charAt(i)) return false;
		
	tokenPos = index;
	tokenLen = len;
	index += len;
	
	return true;
}
```
To jest po prostu:
`Czy kolejne X znaków w oryginalnym JSON-ie są takie same jak słowo 'w'?`
Czyli:
- masz JSON: `"true", "false", "null"`
- masz bufor: `data.charAt(...)`
- masz wzorzec: `"true", "false", "null"`
Nie robisz:
```java
data.substring(index, index + 4).equals("true");
```
bo `substring()` tworzy **NOWY STRING**.
Zbędna alokacja. Wolne. Głupie. Nie chcemy tego.

Więc robimy porównanie znak po znaku.

### A teraz coś, co ci zrobi klik w mózgu:

Wyobraź sobie, że chcesz sprawdzić:
```pgsql
czy data[index..index+3] == "true"
```
Normalnie:
```java
String s = json.substring(index, index+4);
if (s.equals("true")) {...}
```
My robimy to samo, ale bez tworzenia `s`.

Dlatego:
- `w.charAt(i)` -> bierzesz literę z `true`
- `data.charAt(index + i)` -> bierzesz literę z JSON-a
- porównujesz
- jeśli wszystkie takie same -> masz dopasowanie

To jest porównywanie segmentu znaków w tablicy.
"Manualne equals bez tworzenia obiektu"
To jest technika "zero-copy parsing".

I dlatego jest szybkie, bez alokacji, idealne do tokenizerów i parserów - profesjonaliści tak robią.