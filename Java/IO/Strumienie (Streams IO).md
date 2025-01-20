Strumień to jednostronny kanały przepływu danych:
- Dane mogę płynąć w **jedną stronę** do programu **(input)** albo z programu **(output)**.
- Działa to podobnie jak wąż ogrodowy, przez który woda płynie w jedną stronę.

Strumienie pozwalają na:
1. *Odczyt danych* z różnych źródeł, np. plików, klawiatury, sieci.
2. *Zapis danych* do różnych miejsc, np. plików, konsoli, sieci.

***Typy strumieni w Javie***
Java udostępnia dwa podstawowe rodzaje strumieni, które różnią się tym, z jakimi danymi pracują:
- ~={red}Strumienie bajtowe (Byte Streams)=~
	1. Pracują z surowymi bajtami (liczby od 0 do 255).
	2. Używane do przetwarzania danych binarnych, takich jak obrazy, dźwięki, pliki PDF.
	3. Główne klasy:
		- **InputStream do odczytu bajtów**
		- **OutputStream do zapisu bajtów**
- ~={yellow}Strumienie znakowe (Character Streams)=~
	1. Pracują z danymi tekstowymi (znakami Unicode)
	2. Używane do przetwarzania plików tekstowych, konsoli, itp.
	3. Główne klasy:
		- **Reader do odczytu znaków**
		- **Writer do zapisu znaków**

**Kluczowe właściwości strumieni**
1. ~={8}Jednokierunkowość=~: Strumienie mogą działać w jednym kierunku na raz - albo odczyt, albo zapis.
2. ~={green}Sekwencyjność=~ - Dane w strumieniach są przetwarzane w kolejności, w jakiej pojawiają się w źródle (linia po linii, bajt po bajcie, znak po znaku).
3. ~={blue} Blokowanie=~ - Klasyczne IO blokuje program, dopóki operacja odczytu lub zapisu nie zostanie zakończona.