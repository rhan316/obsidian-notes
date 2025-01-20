Przesunięcia bitowe to operacje, które pozwalają manipulować pojedynczymi bitami liczby. W programowaniu często operujemy liczbami na wyższym poziomie (np. całkowitymi (int), zmiennoprzecinkowymi (double)), ale przesunięcia bitowe umożliwiają **precyzyjne kontrolowanie** danych na najniższym poziomie reprezentacji komputera - w formie binarnej.

**Dlaczego przesunięcia bitowe są przydatne?**
1. *Wydajność:* Operacje bitowe są **niesamowicie szybkie**, ponieważ wykonywane są bezpośrednio na poziomie procesora.
2. *Manipulacja danymi:* Przesunięcia bitowe pozwalają na manipulowanie bitami w celu:
	 - *Kompresji danych* (np. zapisywanie wielu informacji w jednym bajcie czy int).
	 - *Szybkich obliczeń matematycznych*, takich jak mnożenie i dzielenie przez potęgi dwójki.
	 - *Efektywnego kodowania/dekodowania*.
	 - Implementowania struktur danych, takich jak *bitmapy*.
3. *Programowanie na niskim poziomie:* W systemach wbudowanych, sterownikach czy grach przesunięcia bitowe są standardem.

*Analogia*
Wyobraź sobie liczbę jako **rząd pudełek**, gdzie każde pudełko może przechowywać jedną kulkę lub nie (0 lub 1). Przesunięcia bitowe to proces przesuwania tych kulek w lewo lub w prawo w pudełkach, co zmienia układ liczb.

**Typy przesunięć bitowych w Javie**
1. `<<` **przesunięcie w lewo** - Wszystkie bity liczby przesuwają się o określoną liczbę miejsc w lewo, a na prawo "wpadają" zera. To jak przesunięcie całego rzędu kulek na lewo, a nowe puste miejsca zapełniamy pustymi pudełkami.
2. `>>` **przesunięcie w prawo** - Przesuwa bity w prawo, zachowując znak (najbardziej lewy bit). To przydatne, gdy chcesz podzielić liczbę przez potęgę dwójki, zachowując znak liczby.
3. `>>>` **Przesunięcie w prawo logiczne** - Przesuwa bity w prawo, a lewe miejsca zawsze zapełnia zerami, niezależnie od znaku. Jest przydatne w pracy z liczbami bez znaku.