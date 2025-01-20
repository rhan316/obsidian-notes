To mechanizm umożliwiający bardziej precyzyjną kontrolę nad hierarchią klas i interfejsów. W skrócie, pozwalają one określić, które klasy mogą dziedziczyć po danej klasie lub implementować dany interfejs.

**Czym są Sealed Classes?**
To klasy, które ograniczają, kto może je rozszerzać lub implementować. Deklaruje się je przy użyciu słowa kluczowego `sealed`, a do definiowania dozwolonych podklas używa się słowa kluczowego `permits`.

```
public sealed class Shape permits Circle, Rectangle {
	// kod klasy
}
```

**Jak działają sealed classes?**
1. **Kontrola dziedziczenia**
	- Klasa `sealed` dokładnie określa, które klasy są dozwolone jako jej podklasy.
	- Możliwe jest ograniczenie rozszerzalności nawet w dużych systemach z wieloma programistami.
2. **Deklaracja podklas** - Podklasy określone w `permits` muszą być albo:
	- `final` - nie mogą być rozszerzane.
	- `sealed` - Mogą dalej kontrolować, kto je rozszerza.
	- `non-sealed` - Mogą być rozszerzane bez ograniczeń.