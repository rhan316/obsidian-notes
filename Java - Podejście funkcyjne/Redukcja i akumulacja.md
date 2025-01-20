**Redukcja** - odnosi się do procesów, w których zbiór danych jest przekształcony w pojedynczy wynik. Typowym przykładem jest sumowanie liczb w tablicy.

**Akumulacja** - to część redukcji, w której dane są zbierane w akumulatorze (zmiennej przechowującej wynik pośredni).

**JS `reduce`**
W JS funkcja `reduce` jest wbudowaną metodą tablicy używaną do redukcji tablicy do pojedynczej wartości.
```
const numbers - [1, 2, 3, 4, 5];

// Redukcja: suma liczb
const sum = numbers.reduce((acc, current) => {
	return acc + current;
}, 0);

console.log(sum); // Wyjście 15
```
`acc` - przechowuje bieżący wynik akumulacji.
`current` - obecny element iterowany.
`0` - początkowa wartość akumulatora.