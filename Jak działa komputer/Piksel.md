***Piksel (ang. pixel = picture + element)*** to najmniejszy punkt obrazu wyświetlanego na ekranie.

### Jak komputer reprezentuje piksele?

Każdy piksel to zbiór liczb reprezentujących jego kolor i jasność.
Najczęściej w formacie:

#### RGB (Red, Green, Blue)
Każdy kolor składa się z 3 składników - po jednym bajcie każdy (8 bitów = 256 poziomów):

| Składnik | Zakres wartości | Przykład              |
| -------- | --------------- | --------------------- |
| Red      | 0 - 255         | 255 = pełna czerwień  |
| Green    | 0 - 255         | 0 = brak zieleni      |
| Blue     | 0 - 255         | 0 = brak niebieskiego |
#### Np. kolor czerwony
```text
RGB(255, 0, 0) -> [0xFF, 0x00, 0x00] -> 3 bajty
```

#### Obraz jako macierz pikseli
Dla komputera obraz to po prostu tablica (macierz) pikseli, np.
$$
image=[(255,0,0)(0,0,255)​(0,255,0)(255,255,255)​]
$$
Każda komórka to wektor `[R, G, B]`. Czyli:
```python
image = [
	[[255, 0, 0], [0, 255, 0]],
	[[0, 0, 255],]
]
```

#### Rozdzielczość

Jeśli ekran ma `1920x1080` pikseli, to:
- To macierz o wymiarach 1080 wierszy i 1920 kolumn.
- Każdy element to np. `[R, G, B]` -> 3 bajty -> 6MB dla jednego obrazu bez kompresji!

#### Format RGBA i inne
Dodajemy kanał przezroczystości (Alpha):
- `RGBA = [R, G, B, A]` -> 4 bajty na piksel
- `A = 0` -> przezroczysty, `A = 255` -> całkowicie widoczny

