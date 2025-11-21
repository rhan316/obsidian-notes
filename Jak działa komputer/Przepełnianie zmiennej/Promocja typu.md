Jeśli wartość nie mieści się w zmiennej danego typu, możemy ją "awansować" (tj. zapisać w większym typie danych) - żeby uniknąć przepełnienia, utraty precyzji lub błędów.
```c
uint8_t a = 255;
uint16_t b = a + 100 // b == 355 -> nie ma overflow, bo typ szerszy
```

### C/C++
- Operacje na typach "mniejszych niż `int`" np. `char, short` promowane są do `int`
- W mieszanych typach np. `int + double`, wynik jest promowany do najszerzej reprezentowanego typu.
```c
char a = 100;
char b = 100;
int c = a + b; // awans do int
```

### Java
- `byte, short, char` -> automatycznie awansowanie do `int` w wyrażeniach arytmetycznych.
- Można ręcznie awansować np. `int -> long`, `int -> double`
- ```java
  byte x = 127;
  byte y = 1;
  // byte z = x + y; // błąd kompilacji!
  int z = x + y; // Ok
  ```