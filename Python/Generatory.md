Generatory w Py to specjalny sposób tworzenia sekwencji danych, który pozwala:
- generować wartości "w locie" (on-the-fly)
- nie trzymać całej listy w pamięci
- pauzować i wznawiać działanie funkcji
- pracować bardzo wydajnie z dużymi danymi.

### 1. Co to jest generator?

Generator to obiekt, który możesz iterować, ale nie trzyma wszystkich wartości  naraz.
Zamiast tego produkuje kolejne wartości wtedy, gdy są potrzebne.

*Generator:*
- pamięta swój stan
- wstrzymuje się przy `yield`
- wznawia od następnej funkcji

### 2. Funkcja z `yield` = funkcja generatora

Gdy w funkcji występuje `yield`, Py zamienia ją w generator:
```python
def counter():
	yield 1
	yield 2
	yield 3
	
Użycie:

for value in counter():
	print(value)

Wynik:
	1
	2
	3
```
Funkcja nie zwraca listy, tylko obiekt generatora.

### 3. Jak działa `yield`?
#### `yield`:
1. Zwraca wartość (tak jak `return`)
2. Pauzuje funkcję
3. po kolejnym żądaniu kontynuuje od miejsca, gdzie przerwała
```c
start -> yield -> pauza -> yield -> pauza -> yield -> koniec
```

### 4. Przykład - licznik do nieskończoności

Generator może być nieskończony (lista nie):
```python
def infinite_counter():
	i = 0
	while True:
		yield 1
		i += 1
```

### Dlaczego generatory są tak ważne?

#### Oszczędzają pamięć
```python
100-milionowy zakres

range(100_000_000)
to generator -> nie zajmuje prawie żadnej pamięci
```

#### Wydajne dla dużych plików
```python
Możesz czytać plik linia po liniii:

def read_file(path):
	with open(path) as f:
		for line in f:
			yield line.strip()
```

#### Lepsze niż list comprehension w wielu sytuacjach
```python
lista:

[x*x for x in range(10)]

generator:

(x*x for x in range(10))

g = (x*x for x in range(5))
for value in g:
	print(value)

Druga wersja nic nie tworzy w pamięci, tylko generuje wartości, gdy są potrzebne
```

### Generator ma specjalne metody
```python
g = counter();

next(g) #1
next(g) #2
next(g) #3

Po użyciu wszystkiego:
StopIteration
```
