***Saturacja*** to zachowanie zmiennej liczbowej przy przepełnianiu, w którym zamiast zawinięcia do zera lub wartości ujemnej, wynik zostaje "nasycony" do maksymalnej lub minimalnej wartości dopuszczalnej.

##### Porównanie:

| Operacja          | Bez saturacji        | Z saturacją |
| ----------------- | -------------------- | ----------- |
| `uint8: 250 + 10` | `4` (bo 260 mod 256) | `255`       |
| `int8: -120 - 10` | `126` (overflow)     | `-128`      |
#### Kiedy i grze używa się saturacji?
- Grafika komputerowa -> RGB kanały muszą być w zakresie `0-255`
- Audio processing -> Głośność, amplituda - nie może wyjść poza (-1, 1)
- Embedded / DSP -> Sygnały czujników, kontrolery PID
- Numeryka -> Ograniczenie błędów przy aproksymacji
- Algorytmy AI -> Clipping wartości wejściowych

