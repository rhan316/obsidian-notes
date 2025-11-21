Każda zmienna typu liczbowego w PC ma ograniczony zakres. Np. `int8 -> -128 do 127`, `uint8 -> 0 do 255`. Przepełnienie to sytuacja , gdy liczba wykracza poza zakres.
```c
int main() {
	unsigned char x = 255;
	x = x + 1; // x == 0 -> przecięcie!
	printf("%u\n", x);
}
```
- `unsigned char` (8 bitów) ma zakres `0-255`
- `255 + 1 = 256`, ale nie da się zapisać w 8 bitach
- Wynik: 256 mod 256 = 0 -> przecięcie do najniższych 8 bitów

### Co to jest "przycięcie" (truncation)?
To zachowanie, w którym nadmiar bitów po prostu się obcina.
Przykład binarnie (8 bitów):
```text
x = 11111111  (255)
x + 1 = 1 00000000  (256 → 9 bitów!)
Przcięcie do 8 bitów: 00000000 → 0
```

##### Dlaczego to nie jest błąd w C/C++?
W językach takich jak C, overflow dla typów bez znaku `unsigned` jest zdefiniowane jako modulo, więc:
```c
unsigned int a = UINT_MAX;
a++; // Ok, zawija się do 0
```
Dla typów signed, przepełnienie jest niezdefiniowane (UB - undefined behavior), co może prowadzić do błędów lub exploitów!

#### Przykład przycięcia w typach
```java
byte b = (byte) 130;
print(b); // wypisze -126
```
- `130 -> 10000010` (8 bitów)
- Jako `byte` (signed) -> odczytywanie jako `-126` (Two's complement)
- Przycięcie + reinterpretacja = niespodzianka!

