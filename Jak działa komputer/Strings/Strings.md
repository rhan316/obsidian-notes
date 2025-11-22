String to ciąg znaków, ale pod spodem jest to:
Tablica (ciąg) bajtów, które reprezentują znaki, zakończona lub opisana długością w zależności od języka programowania.

### Na poziomie maszyny:
- Każdy znak to bajt (w ASCII) lub sekwencja bajtów (w UTF-8, UTF-16 itd.).
- String to ciąg bajtów w pamięci.
- Potrzebujemy czegoś, co określi gdzie kończy - stąd dwie główne strategie:
```C
null-terminated strings

char* s = "hello";
W pamięci: ['h', 'e', 'l', 'l', 'o', '\0']
Specjalny znak '\0' (null) to koniec stringa.
```
Wady:
- trzeba skanować cały ciąg, żeby znać długość O(n)
- nie można mieć `\0` w środku
- łatwo o błędy bezpieczeństwa (np. przepełnienie bufora)

```java
length-prefixed objects

String s = "hello";
W pamięci: obiekt zawierający:
- wskaźnik do tablicy znaków (UTF-16)
- pole `length`
- często cache dla hashCode
  
Struktura:

class String {
	final char[] value;
	final int length;
}
```
Zalety:
- działa z dowolnymi znakami (Unicode)
- szybki dostęp do długości
- niemutowalność ułatwia bezpieczne współdzielenie

