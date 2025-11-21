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