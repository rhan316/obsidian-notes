
Wymagają specjalnego formatu -> ***Format IEEE 754*** - standard liczb zmiennoprzecinkowych.
To oficjalny i powszechnie używany sposób reprezentowania liczb rzeczywistych w komputerach.

#### Np. 32-bitowy (Single Precision) format IEEE 754
Składa się z 3 części:

| Bity | Znaczenie                | Liczba bitów |
| ---- | ------------------------ | ------------ |
| `s`  | Znak (0 = +, 1 = -)      | 1 bit        |
| `e`  | Wykładnik (biasowany)    | 8 bitów      |
| `m`  | Mantysa (część ułamkowa) | 23 bity      |
### Reprezentacja liczby:

Liczba `x` jest przechowywana jako:

		$x=(−1)s⋅1.m⋅2(e−127)$

s -> znak
1.m -> mantysa z ukrytą jedynką (tzw. normalized form)
e - 127 -> wykładnik, z tzw. biasem (domyślnie 127)

### Przykład: 5.375

*Krok 1: Zmiana na postać binarną*

$$
\begin{aligned}
\text{Liczba:} &\quad 5.375 \\
\text{Postać binarna:} &\quad 101.011_2 = 1.01011 \cdot 2^2 \\
\\
\text{Znak (s):} &\quad 0 \quad (\text{liczba dodatnia}) \\
\text{Wykładnik (e):} &\quad 2 + 127 = 129 \Rightarrow 10000001_2 \\
\text{Mantysa (m):} &\quad 01011000000000000000000 \\
\\
\text{IEEE 754 (32-bit):} &\quad 
\underbrace{0}_{\text{znak}} \;
\underbrace{10000001}_{\text{wykładnik}} \;
\underbrace{01011000000000000000000}_{\text{mantysa}} \\
&= 0\;10000001\;01011000000000000000000
\end{aligned}
$$

### Mantysa = znaczące cyfry liczby (po przecinku)

W przypadku IEEE 754:
- Reprezentuje *część ułamkową* liczby binarnej.
- Nie zawiera pierwszej `1`, bo t jest domyślna (implicit leading one), tzn. zawsze zakładamy, że liczba ma postać `1.xxxxx`.

#### Krok 1: Binarna postać:
$$
\begin{aligned}
\text{Postać binarna:} &\quad 101.011_2 = 1.01011 \cdot 2^2 \\
\end{aligned}
$$
##### Krok 2: Mantysa
- Po przecinku mamy: `01011`
- W formacie IEEE 754 zapisujemy tylko to, co jest po przecinku, czyli
		`01011000000000000000000` (dopełnione zerami do 23 bitów)

#### Intuicyjnie
Mantysa mówi: "Jakie są najważniejsze cyfry tej liczby?"
W systemie dziesiętnym: 
$$
\begin{aligned}
\text{W liczbie: } 1.2345 \cdot 10^3 -> mantysa &\ to \ 1.2345
\end{aligned}
$$
W binarnym: `1.01011` -> mantysa to `01011` (bo `1.` jest ukryte).

Mantysa to zakodowana część znaczących cyfr binarnych liczby zmiennoprzecinkowej.
W IEEE 754 zapisujemy ***tylko część ułamkową*** po przecinku binarnym (bo całkowita 1 jest ukryta). Dzięki temu oszczędzamy miejsce i zyskujemy precyzję!