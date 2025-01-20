Monitor w Javie to mechanizm wbudowany w każdy obiekt, który pozwala synchronizować dostęp do kodu lub zasobów współdzielonych przez wiele wątków. Jest jak *zamknięte pomieszczenie, do którego może wejść tylko jeden wątek na raz*, a reszta musi czekać na zewnątrz.

**Jak działa monitor**

1. **Blokada obiektu (lock):** Każdy obiekt w Javie ma jedną unikalną blokadę. Gdy wątek chce wykonać synchronizowany blok lub metodę, próbuje uzyskać dostęp do blokady monitora tego obiektu. Jeśli blokada jest dostępna (niezajęta przez inny wątek), wątek ją "zdobywa" i wchodzi do monitora. Jeśli blokada jest zdjęta, wątek musi czekać.
2. **Jeden wątek na raz**: Tylko jeden wątek może wykonywać kod chroniony monitorem danego obiektu w danym momencie.
3. **Oddanie blokady**: Po zakończeniu wykonywania synchronizowanego bloku/metody wątek zwalnia blokadę, co pozwala innemu wątkowi wejść do monitora.

**Gdzie monitor jest używany?**
Monitor jest aktywnie wykorzystywany, gdy stosujemy:
```
1. Słowo kluczowe synchronized
	public synchronized void method () {};

2. W blokach synchronizowanych
	synchronized (this) {};

3. Metody wait(), notify(), notifyAll() - te metody wykorzystują monitor obiektu i mogą być wywoływane tylko wewnątrz synchronizowanego bloku lub metody.
```

*Analogia*
Wyobraź sobie firmę, w której znajduje się jeden pokój do składania zamówień (monitor). Tylko jeden pracownik (wątek) może wejść do pokoju na raz, żeby złożyć zamówienie.
- Jeśli drzwi są otwarte (blokada dostępna), pracownik wchodzi do środka i wykonuje swoje zadanie.
- Jeśli drzwi są zamknięte (blokada zdjęta), kolejny pracownik musi czekać na zewnątrz, aż poprzedni skończy i wyjdzie.
