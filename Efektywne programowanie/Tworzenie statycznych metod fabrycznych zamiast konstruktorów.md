
**Wzorzec projektowy "metoda fabryczna" nie jest tym samym co statyczna metoda fabryczna!!!**

*Statyczna metoda fabryczna* to zwykła metoda fabryczna zwracająca obiekt tej klasy.

```
public static Boolean valueOf(boolean b) {
	return (b ? Boolean.TRUE : Boolean.FALSE)
};
```

1. **Konstruktory nie zawierają nazw (do czego służą), statyczne metody fabryczne zawierają nazwę informującą jaki obiekt zostanie zwrócony.**
2. **Przy tworzeniu SMF, nie jest wymagane budowanie nowego obiektu podczas wywołania metody.**
3. **Kontrola klas przez instancje**
   - Gwarancja zastosowania singleton
   - Upewnianie się, że nie istnieją 2 takie same obiekty
4. **Metody zwracają typ, który jest podtypem zwracanego typu.**
5. **Wymusza podanie interfejsu jako zwracany obiekt, a nie przez klasę.**
6. **Różne atrybuty - inny zwracany obiekt**
7. **Klasa obiektu zwracanego nie musi jeszcze istnieć